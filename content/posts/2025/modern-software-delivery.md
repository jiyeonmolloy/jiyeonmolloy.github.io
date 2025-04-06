---
date: '2025-04-06T16:16:34+12:00'
draft: false
title: 'Demystifying Modern Software Delivery: Trunk-Based Development, CI/CD, and Releases 🚀👨🏻‍🚀'
categories: ["software delivery", "trunk-based development", "tdd", "continuous deployment", "continuous delivery", "deployment", "release", "tips", "software engineers"]
---

![alt text](/assets/images/tbd-eevee-charizard.png)

Software delivery has changed a lot over the years! What’s the difference between **continuous delivery** and **continuous deployment**? 🤔

And is a feature `live` just because it’s deployed? 🤨

Let’s look into this together with some modern DevOps 🚀

---

## 🌳 Trunk-Based Development

Trunk-based development (TBD) is a software development strategy where everyone works from a single branch (trunk) — usually `main`. It’s fast, lean, and fits in modern delivery practices.

### 🔧 How it works:
- Developers commit to `main` (or short-lived branches that are merged quickly to the `main` branch)
- The `main` branch is always deployable
- Features are hidden behind flags until they’re ready to go live 🚀

### 💡 Why it matters:
Trunk-based development encourages:
- Fewer merge conflicts 🙅‍♂️
- Smaller, safer changes ✅
- Faster feedback loops 🔁

### ✅ Core Principles of TBD
1. Single source of truth: All changes go through the trunk (usually `main`)
2. Short-lived branches (if any): Avoid long-running feature branches. Merge fast! 🏃🏻‍♂️
3. Continuous integration: Changes are merged and tested constantly
4. Always deployable: The trunk is always in a releasable state — even if features are hidden behind flags

This helps set-up a clean, automated release process 😎

![alt text](/assets/images/eevee-and-charizard-in-rocket-space.png)

## 🧱 Continuous Delivery vs 🚀 Continuous Deployment

We often use these terms interchangeably, but they’re **not** the same thing. Let’s break it down 👇

|                      | **Continuous Delivery** 🧺           | **Continuous Deployment** 🔄       |
|----------------------|--------------------------------------|------------------------------------|
| Code goes to prod?   | *Only if you say so* 🖱️             | *Automatically!* 😊 Yay!              |
| Human involvement?   | Yes – manual release decision 🙋‍♀️ | Nope – all tests pass? It ships 🚢 |
| Speed to users       | Fast ⚡️                            | Fastest 🚀                         |
| Risk level           | Lower (more control) 🧯             | Higher (but with confidence!) 💪   |

### 🎯 TL;DR:
> **Continuous Delivery** = Code is *ready* to go live.  
> **Continuous Deployment** = Code *automatically* goes live.

## 🕵️ Deployment vs 🎉 Release

Just because your code is **deployed** doesn’t mean it’s **released**. Let’s look into this further together:

### 👩🏻‍🚀 Deployment
- Code is in `production` 🖥️
- But might be hidden behind a feature flag 🏁
- Invisible to users 👻

### 🏃🏻‍♀️ Release
- Users can *see* and *use* the new feature 🥳
- Controlled by toggles, permissions, or gradual rollouts 🔦

### 📦 Example:
You deploy a new dark mode toggle 🌙 — the code is live but hidden.  
Later, you release it to users by flipping a switch 🔛.

## 🔄 Why Separating Deployment and Release is Helpful

- **Safer launches** 🚧  
- **Gradual rollouts** (hello canary releases 🐤, blog coming soon to talk more about this!)  
- **Fast recovery** – you can turn features off without re-deploying 🔙  

## 🌟 Wrapping Up

Modern software delivery is all about small, safe, and speedy changes.  

Remember:
> ✅ Deployed doesn’t mean released!
> 🚀 Deployment isn’t delivery  
> 🧠 Fast delivery is a mindset, not just a tool

Have a nice day 🥰