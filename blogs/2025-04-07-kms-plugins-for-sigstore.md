---
title: "KMS Plugins for Sigstore"
url: "https://blog.sigstore.dev/kms-plugins/"
date: "Mon, 07 Apr 2025 00:00:00 UTC"
author: ""
feed_url: "https://blog.sigstore.dev/index.xml"
---
Cosign and private deployments of Fulcio and Rekor can use a KMS-managed key for signing artifacts. We currently have built-in support for AWS, Azure, Google Cloud Platform, and Hashicorp Vault KMSs. This has been a challenge for customers that require alternative or custom KMS solutions.
To enable such use-cases, we have implemented a new plugin system for alternate KMS providers. Organizations can independently and privately develop &amp; distribute their plugins without needing downstream updates to libraries to support additional KMS providers as build-time dependencies.
