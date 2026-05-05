---
title: "Introduction sigstore-c"
url: "https://blog.sigstore.dev/sigstore-c/"
date: "Wed, 01 Apr 2026 00:00:00 UTC"
author: ""
feed_url: "https://blog.sigstore.dev/index.xml"
---
These days, there&rsquo;s many interoperable Sigstore client libraries in various programming languages. But there are still a few places where you might struggle to run Sigstore, like on a Intel 8086 processor (first released in 1978), say running a version of DOS.
Until today. Introducing sigstore-c, which focuses on portability over features (and correctness!)
You can build sigstore-c on any system with a C89 compiler, including modern Linux environments with gcc or the aforementioned DOS environment with something like Open Watcom v2.
