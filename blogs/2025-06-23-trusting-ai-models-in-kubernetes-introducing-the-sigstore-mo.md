---
title: "Trusting AI Models in Kubernetes: Introducing the Sigstore Model Validation Operator"
url: "https://blog.sigstore.dev/model-validation-operator-v1.0.1/"
date: "Mon, 23 Jun 2025 00:00:00 UTC"
author: ""
feed_url: "https://blog.sigstore.dev/index.xml"
---
As machine learning becomes deeply embedded in critical infrastructure, the question of trust in deployed models is increasingly critical. How can we be sure that an AI model running in a Kubernetes cluster is exactly what it claims to be?
The OpenSSF AI/ML working group believes the answer can be found in signing AI models. A long-standing practice in traditional software distribution is to leverage cryptographic signatures to help end-users verify provenance: that software is authentic, has not been tampered with, and was authored by the expected creator.
