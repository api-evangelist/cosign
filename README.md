# Cosign (cosign)

Cosign is the command-line client of the Sigstore project for signing, verifying, and storing container images, OCI artifacts, blobs, and in-toto attestations. Cosign supports keyless signing via OIDC identity providers, short-lived certificates from Fulcio, and transparency log recording in Rekor.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/cosign/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Provider
- **Access:** Public
- **x-type:** opensource

## Tags

- Apache 2.0, Attestations, CLI, Code Signing, Containers, Fulcio, Go, Keyless, OCI, OIDC, Open Source, Rekor, Sigstore, Supply Chain, Transparency Log, Verification

## Timestamps

- **Created:** 2026-03-26
- **Modified:** 2026-04-28

## APIs

### Cosign CLI

Command-line tool for signing, verifying, and storing container images and OCI artifacts. Supports keyless signing, hardware keys, KMS providers, attestations, and transparency log inclusion.

- [Documentation](https://docs.sigstore.dev/cosign/)
- [Getting Started](https://docs.sigstore.dev/quickstart/quickstart-cosign/)
- [GitHub](https://github.com/sigstore/cosign)
- [Reference](https://docs.sigstore.dev/cosign/reference/cosign/)

### Sigstore Rekor API (consumed)

Public Sigstore transparency log REST API that cosign writes to and reads from when recording and verifying signing events.

- [Documentation](https://docs.sigstore.dev/logging/overview/)
- [OpenAPI](https://raw.githubusercontent.com/sigstore/rekor/main/openapi.yaml)
- [GitHub](https://github.com/sigstore/rekor)

### Sigstore Fulcio API (consumed)

Public Sigstore code-signing certificate authority that issues short-lived X.509 certificates bound to OIDC identities for keyless signing.

- [Documentation](https://docs.sigstore.dev/certificate_authority/overview/)
- [GitHub](https://github.com/sigstore/fulcio)

## Common Properties

- [Website](https://www.sigstore.dev/)
- [Documentation](https://docs.sigstore.dev/cosign/)
- [Getting Started](https://docs.sigstore.dev/quickstart/quickstart-cosign/)
- [Installation](https://docs.sigstore.dev/cosign/system_config/installation/)
- [GitHub Repository](https://github.com/sigstore/cosign)
- [Blog](https://blog.sigstore.dev/)
- [License](https://github.com/sigstore/cosign/blob/main/LICENSE)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
