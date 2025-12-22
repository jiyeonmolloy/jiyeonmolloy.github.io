---
date: '2025-12-22T15:38:23+11:00'
draft: false
title: '🚀 Scaling smarter on Kubernetes: A beginner friendly look at KEDA & Karpenter ✨'
categories: ["KEDA", "karpenter", "kubernetes", "k8s", "AWS", "software engineers", "tips", "autoscaling"]
---
![alt text](/assets/images/eevee-keda-charizard-karpenter.png)

Helloo!

If you have ever run apps on Kubernetes, you will know that scaling is one of the most powerful features it gives you. But once you go beyond simple CPU-based autoscaling, things can definitely get a bit trickier.

That is where [KEDA](https://keda.sh/) and [Karpenter](https://karpenter.sh/) come in! Two really awesome open-source tools that bring smarter, faster, and more cost-friendly scaling to your clusters. In this post, we will take a beginner friendly tour of what they do, how they work, and why teams (including ours!) love them 💛

## 💡 Real life analogy with people & houses 🏠👨‍👩‍👧‍👦

Before we dive deeper into the techie side, let’s visualise it together in something that's easy to relate to:

### 🧍‍♂️ Think of pods as people
These are the individual workers in your system — like people doing our jobs.

### 🏠 Think of nodes as houses
These are where people live and work (working from home 😉💻). So, if you have more people, you might need more houses.

Using this analogy:

KEDA is like the event planner and town co-ordinator: watching how busy things are and calling in (or sending away) people as required.

Karpenter is like the property developer and builder 🔨 It makes sure the town has enough houses for everyone, and it regularly re-builds older houses with improved materials, fixing leaks and updating house locks along the way 🔐. In Kubernetes terms, that means rolling nodes to apply new AMIs, patches, and security updates automatically.

## 🌱 What is KEDA?

[KEDA (Kubernetes Event-Driven Autoscaling)](https://keda.sh/) is an add-on that helps Kubernetes scale your workloads based on events, not just CPU or memory. KEDA works alongside standard K8s components like HPA ([Horizontal Pod Autoscaler](https://kubernetes.io/docs/concepts/workloads/autoscaling/horizontal-pod-autoscale/)) and can further extend the functionalities.

Think of the town co-ordinator 👩‍💼 they don’t just count CPU usage, they look at meaningful signals like:

- 📬 how many messages are waiting in a queue
- 🌐 how many HTTP requests are happening right now
- 📊 metrics from tools like [New Relic](https://newrelic.com/)

and lots more with its [scalers](https://keda.sh/docs/2.18/scalers/)

## ✨ Why teams love KEDA 💟
### 🌟 Scale to ZERO 🧹

KEDA can actually scale a workload down to 0 pods when nothing is happening, just like sending everyone home when the town gets quiet. With HPA it wasn't possible to scale down to 0 as metrics such as CPU or memory cannot be 0.

This means:

- 💸 No idle cost
- 💤 No extra pods sitting around
- 💻 You only run compute when it is required

This is especially great for batch jobs, event-driven systems, or workloads that only run occasionally.

### 📈 Lots of scalers available

KEDA comes with a huge library of scalers so you can scale on lots of different signals, not just CPU or memory:

- ☁️ AWS SQS – based on queue length
- 🌐 HTTP requests – based on in-flight requests
- 📊 New Relic – based on custom app metrics

This flexibility makes KEDA very useful for real-world workloads.

### 🏗 What is Karpenter?

While KEDA helps you scale pods (people 😉), the town still needs nodes (houses 🏠) to put those people in.

Karpenter is a fast, flexible autoscaler for Kubernetes nodes, like a property developer who builds new houses quickly and efficiently when more people arrive.

Karpenter can:

- ⚡ Provision new houses really fast
- 🧠 Pick the right type of house for the job
- 💸 Helps reduce wasted cost by choosing efficient options
- 🎯 Set preferences (e.g. use Spot instances first)

So if your town suddenly gets busy, Karpenter makes sure there are enough houses for everyone, without you needing to manually plan each one.

### 🧩 KEDA + Karpenter working together 🤝🏻

Together, they create a super smooth autoscaling pipeline:

Users → Traffic spikes → KEDA scales pods → Karpenter adds houses → Smoother performance ✨

Also in reverse 😉:

Quiet town → KEDA scales to zero pods → Karpenter removes unused houses → Lower costs 💵

This often leads to:

- 💰 Cost savings
- 💤 Reduced operational overhead
- 🚀 More responsive applications

### 🌩️ Running KEDA & Karpenter on AWS EKS

Both KEDA and Karpenter work really well on Amazon EKS, and that is how many teams (including ours!) run them in production. KEDA integrates with AWS services like SQS or CloudWatch for event-driven autoscaling, while Karpenter can give you fast EC2 provisioning, Spot capacity awareness and automatic node rolling with updated AMIs.

### 🤶🏻 Wrapping up!

KEDA and Karpenter are two amazing tools in the Kubernetes ecosystem. They are incredibly powerful, and helps us unlock smarter scaling patterns that bring big wins in cost, performance, and simplicity. Please watch this space for follow on blog posts to dive deeper into KEDA and Karpenter 😊 Also, it's nearly Christmas so hope everyone has a nice Christmas and end of year holidaays! 🎄
