---
title: "Rekor v2 - Cheaper to run, simpler to maintain"
url: "https://blog.sigstore.dev/rekor-v2-alpha/"
date: "Thu, 17 Apr 2025 00:00:00 UTC"
author: ""
feed_url: "https://blog.sigstore.dev/index.xml"
---
We are very excited to announce the alpha release of Rekor v2!
Rekor v2 is a redesigned and modernized Rekor, Sigstore&rsquo;s signature transparency log, transitioning its backend to a modern, tile-backed transparency log implementation to simplify maintenance and lower operational costs.
Major changes include:
A new storage backend, replacing Trillian with Trillian-Tessera. Tile-based logs are cheaper to run and easier to deploy, maintain and scale. To learn more about the benefits of tile-based logs, read this blog post A redesigned and simplified API, using the learnings from operating public-good Rekor over the past 2 years Stronger security guarantees that the log remains append-only by integrating witnessing directly into Rekor (To be implemented) For the initial release, we are providing a binary and container for developers.
