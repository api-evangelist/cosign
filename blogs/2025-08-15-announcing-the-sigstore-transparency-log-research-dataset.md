---
title: "Announcing the Sigstore Transparency Log Research Dataset"
url: "https://blog.sigstore.dev/rekor-bigquery-dataset/"
date: "Fri, 15 Aug 2025 00:00:00 UTC"
author: ""
feed_url: "https://blog.sigstore.dev/index.xml"
---
We&rsquo;re pleased to announce the creation of a new BigQuery public dataset, rekor. The rekor dataset is an easily-queryable mirror of the public good instance of Sigstore&rsquo;s transparency log, Rekor.
As a reminder, signing events are recorded in Rekor, Sigstore&rsquo;s append-only transparency log. Software consumers rely on cryptographic proofs of log inclusion to verify that software artifacts are recorded to the log. Software producers can verify metadata in the log, verifying that the recorded signature metadata was produced as expected when their identities or keys were used to sign artifacts, using a Rekor monitor.
