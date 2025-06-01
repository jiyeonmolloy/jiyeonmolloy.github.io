---
date: '2025-06-01T15:48:25+12:00'
draft: false
title: '🚢 Kubernetes 101: Book Recommendations, K8s Basics with Pokémon, and Getting Started! 🐾🐳'
categories: ["kubernetes", "k8s", "probes", "nigel poulton", "tips", "pokemon", "software engineers"]
---

![alt text](/assets/images/eevee-and-charizard-the-kubernetes.jpg)

## 📚 Let's Start With a Book!

I highly recommend The [Kubernetes Book by Nigel Poulton](https://goodreads.com/book/show/35494978-the-kubernetes-book). It’s beginner-friendly, concise, and full of real world insights. It's a great starting point when learning about Kubernetes.

## 🌍 Where Did the Word Kubernetes Come From?
The word `Kubernetes` (pronounced Q-ber-net-ees) comes from Greek, meaning helmsman or pilot of a ship ⛵. We often use `K8s` as a shorthand to refer to Kubernetes! This is because there are 8 letters between `K` and `s`.

## 📦 Pods, Services, and Deployments ✨
- **Pods** are like shipping boxes 📦 for your app, they are the smallest deployable unit in Kubernetes and act as a wrapper around one or more container(s)
- **Services** are like traffic routers 📡! They give your app a stable IP or DNS name and forward requests to the right Pod, even if the Pod’s IP changes. They are how other services (or users via Ingress) reliably find your app
- **Deployments** let you roll out changes easily. Want a new version? Push the update and Kubernetes slowly swaps old pods 📦 for new ones 🌀

☁️ Kubernetes is **declarative**, meaning you describe your desired state and it works hard to match it 🎁.

## 🐶 Probes: Is Your App Ready?
![alt text](/assets/images/eevee-and-charizard-playing.jpg)

Kubernetes has three types of health probes that help it understand how your application (Pod) is doing. 
To make this more relatable, let’s use [eevee](https://pokemondb.net/pokedex/eevee) 🐕💕

### 🍼 Startup Probe –  Is Eevee done evolving? 💎
When a Pod first starts, it might take some time to become stable - like when Eevee is evolving to e.g. [Vaporeon](https://pokemondb.net/pokedex/vaporeon) or [Flareon](https://pokemondb.net/pokedex/flareon) 🔥💧.

📘 Example:
A backend service might take 30 seconds to warm up. If you probe it too soon, it looks broken, but it’s just finishing initial setup. The startup probe prevents other probes from running too early and potentially killing the pod.

### 🟢 Readiness Probe – Is Eevee ready to battle? 🥊
Even after evolving, Eevee might need a quick heal at the Pokémon Center ⚕️ or a bit of training before it can battle.
Readiness probes check whether the pod is fully prepared to receive traffic.

📘 Example:
A web server pod starts up but needs to establish a DB connection first. Until it’s ready, Kubernetes won’t route requests to it.

### ❤️ Liveness Probe – Has Eevee fainted in battle? 😿
Sometimes, a Pod just stops responding altogether and it’s like when Eevee fainted in the middle of a Pokémon battle 😢.
Liveness probes make sure the Pod is still functioning. If not, Kubernetes restarts it.

📘 Example:
A pod might deadlock and stop responding. The liveness probe detects this and restarts the container.

## 📉 Pod Disruption Budgets 🐾
You don’t want all your pods going down during updates. A Pod Disruption Budget (PDB) sets limits like: "At least 1 pod must stay running" 🛡️ similar to having at least one Pokémon being out in the battle field.

This helps maintain availability during voluntary disruptions (like rolling updates or node maintenance).

## 🎉 Wrapping Up: You now know the K8s Basics! 📦
You now know:

- What Pods, Services, and Deployments are and how they work together 🤝
- How Kubernetes uses probes (like readiness and liveness) to check if your app is healthy 🧪
- How Pod Disruption Budgets help keep your app available during changes 🛡️
- Why Kubernetes is all about declarative configuration: you say what you want, and Kubernetes figures out how to make it happen ⚙️

More Kubernetes blogs coming soon 🚀👩🏻‍🚀