---
date: '2025-05-18T20:55:52+12:00'
draft: false
title: '🔐 No More Secrets 😎 Secure GCP Auth from GitHub Actions using Workload Identity Federation'
categories: ["github actions", "google cloud", "workload identity federation", "tips", "security", "auth", "software engineers"]
---

[TODO] - INSERT PIC

In the world of CI/CD, one thing we are all tired of is managing long-lived service account keys. 
They are hard to rotate.. risky to store, and can lead to serious breaches if leaked! 😿

In this post, I will be showing how to set up GitHub Actions + [Google Cloud Workload Identity Federation (WIF)](https://cloud.google.com/iam/docs/workload-identity-federation) to enable secure, short-lived authentication, with no secrets stored anywhere. 🚫🔑

### 🚨 The Problem with Static Secrets
It is still common to authenticate from GitHub Actions to GCP using service account keys stored as GitHub secrets:

```bash
echo "${{ secrets.GCP_KEY }}" > key.json
gcloud auth activate-service-account --key-file=key.json
```

This approach works, but it has downsides such as:

- 🔑 Long-lived credentials: valid for months or years
- 💥 Risk of leakage
- 🔁 Manual rotation or forgotten rotation 😬
- 📦 Secrets management overhead

### ✅ The Better Way: Workload Identity Federation 💌

Instead of storing credentials, we can let GitHub Actions request an identity token at runtime, and have GCP validate that token and issue a short-lived access token.

This is made possible using:

- [OpenID Connect (OIDC)](https://docs.github.com/en/actions/security-for-github-actions/security-hardening-your-deployments/about-security-hardening-with-openid-connect): A standard that GitHub supports natively
- [Workload Identity Federation](https://cloud.google.com/iam/docs/workload-identity-federation): A GCP feature that lets you trust identities from external providers (like GitHub)

### 🛠️ How It Works

Let’s walk through the high-level flow!

![How GitHub Actions OIDC Works with GCP](https://storage.googleapis.com/gweb-cloudblog-publish/images/2_GitHub_Actions.max-1100x1100.jpg)
*Source: [Google Cloud Blog](https://cloud.google.com/blog/products/identity-security/enabling-keyless-authentication-from-github-actions)*

- ✅ GitHub Actions requests an OIDC token signed by GitHub
- 🌍 This token is sent to GCP’s Security Token Service (STS)
- 🔐 GCP verifies the token and exchanges it for a short-lived access token
- 🚀 Your Action uses this token to call GCP APIs & no secrets involved

### 🧩 Setting It Up (High-Level)
1. Create a Workload Identity Pool & Provider in GCP

```bash
gcloud iam workload-identity-pools create github-pool \
  --location="global" \
  --display-name="GitHub Actions Pool"

gcloud iam workload-identity-pools providers create-oidc github-provider \
  --location="global" \
  --workload-identity-pool="github-pool" \
  --display-name="My GitHub Provider" \
  --attribute-mapping="google.subject=assertion.sub,attribute.repository=assertion.repository" \
  --issuer-uri="https://token.actions.githubusercontent.com"
```

2. Create a Service Account and Allow GitHub to Impersonate It

```bash
gcloud iam service-accounts create gha-deploy

gcloud iam service-accounts add-iam-policy-binding gha-deploy@YOUR_PROJECT.iam.gserviceaccount.com \
  --role="roles/iam.workloadIdentityUser" \
  --member="principalSet://iam.googleapis.com/projects/PROJECT_NUMBER/locations/global/workloadIdentityPools/github-pool/attribute.repository/my-org/my-repo"
```

3. Configure GitHub Actions
Please see: https://github.com/google-github-actions/auth

In your workflow:

```yaml
permissions:
  id-token: write
  contents: read

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: 'actions/checkout@v4'

      - name: Authenticate to GCP
        uses: google-github-actions/auth@v2
        with:
          token_format: "access_token"
          workload_identity_provider: "projects/PROJECT_NUMBER/locations/global/workloadIdentityPools/github-pool/providers/github-provider"
          service_account: "gha-deploy@YOUR_PROJECT.iam.gserviceaccount.com"
```

Now you now have short-lived credentials, scoped precisely to your repository and branch 😎

### 🔐 Locking It Down: Use GitHub OIDC Attributes for Fine-Grained Access
GitHub's OIDC tokens come with a set of useful claims. When you configure your provider in GCP, you can map these claims to attributes, and then use those attributes to control who gets access to impersonate your service account.

### 📋 Common GitHub Claims

| Claim            | Description                                                      |
|------------------|------------------------------------------------------------------|
| sub              | e.g. repo:my-org/my-repo:ref:refs/heads/main                     |
| repository       | my-org/my-repo                                                   |
| ref              | refs/heads/main, refs/tags/v1.0.0, etc                           |
| workflow         | .github/workflows/deploy.yml                                     |
| job_workflow_ref | my-org/my-repo/.github/workflows/deploy.yml@refs/heads/main      |
| actor            | The GitHub user who triggered the workflow  😁                  |

### 🗺️ Example Attribute Mapping

You can map these into usable GCP attributes when creating the provider:

```bash
--attribute-mapping="google.subject=assertion.sub,attribute.repository=assertion.repository,attribute.ref=assertion.ref,attribute.workflow=assertion.workflow,attribute.actor=assertion.actor"
```

### 🔒 Use Conditions to Restrict Access

Now you can enforce specific conditions when assigning access:

🌟 Restrict to a specific repo
```bash
principalSet://.../attribute.repository/my-org/my-repo
```

🌟 Restrict to a repo and branch
```hcl
attribute.repository == "my-org/my-repo" &&
attribute.ref == "refs/heads/main"
```

🌟 Restrict to a specific workflow file
```hcl
attribute.workflow == ".github/workflows/deploy.yml"
```

🌟 Restrict to a specific actor (user/bot)
```hcl
attribute.actor == "deploy-bot"
```

### 🧱 Putting It in Practice
```bash
gcloud iam service-accounts add-iam-policy-binding gha-deploy@your-project.iam.gserviceaccount.com \
  --role="roles/storage.admin" \
  --member="principalSet://iam.googleapis.com/projects/PROJECT_NUMBER/locations/global/workloadIdentityPools/github-pool/attribute.repository/my-org/my-repo" \
  --condition="expression=attribute.ref=='refs/heads/main' && attribute.workflow=='.github/workflows/deploy.yml'"
```

Now only your `deploy.yml` workflow on the main branch can assume this identity. 🔒✨

### 🧠 Federation ≠ Impersonation
Workload Identity Federation lets GCP trust an external identity (like GitHub) without the external system needing any GCP credentials. Think of it like: “GitHub says this workflow is running, and GCP trusts that, so GCP hands back a short-lived access token.” 🤝🏻

It's similar to assuming a role in AWS, but uses open standards like OIDC and token exchange (STS).

### 🎯 Benefits Recap
- ✅ No stored secrets
- ✅ Short-lived, scoped credentials
- ✅ Fine-grained access with identity claims
- ✅ Multi-cloud ready (also available in AWS, Azure)

### 🙌 Final Thoughts
This pattern is fast becoming the new standard for CI/CD authentication in cloud-native platforms. It’s simpler, safer, and aligns well with platform engineering principles.

If your team is still managing static service account keys in CI — give this a try 🚀