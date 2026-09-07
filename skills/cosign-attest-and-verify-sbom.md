---
generated: '2026-09-07'
method: generated
name: Attest an SBOM and verify it
description: >-
  Attach a signed in-toto attestation carrying an SBOM to a container image, then verify and read it
  back.
api: cli/cosign-cli.yml
operations: [cosign attest, cosign verify-attestation, cosign download attestation, cosign tree, cosign clean]
source: >-
  Grounded in the published CLI reference at https://github.com/sigstore/cosign/tree/main/doc
  (doc/cosign_attest.md, doc/cosign_verify-attestation.md, doc/cosign_download_attestation.md) and
  the project's own specs — specs/ATTESTATION_SPEC.md, specs/SBOM_SPEC.md, specs/BUNDLE_SPEC.md.
---

# Attest an SBOM and verify it

An attestation is a DSSE-wrapped in-toto Statement (payload type `application/vnd.in-toto+json`)
signed the same way a signature is, and stored as a Sigstore bundle
(`application/vnd.dev.sigstore.bundle.v0.3+json`) alongside the image per OCI Image Manifest v1.1.
See `data-model/cosign-data-model.yml`.

The standalone `cosign attach sbom` / `--type sbom` path is deprecated. Carry the SBOM in an
attestation.

## Auth
Same as signing — an OIDC identity (or a key/KMS/hardware identity) plus registry write permission.

## Steps

1. **Produce the SBOM** with your scanner of choice, in SPDX or CycloneDX JSON.

2. **Attest it.** `cosign attest --predicate <sbom.json> --type <spdxjson|cyclonedx> <IMAGE>@sha256:…`
   Same permanence rules as signing: keyless attestation writes a permanent public Rekor entry.

3. **Verify it.** `cosign verify-attestation --type <same type> --certificate-identity-regexp … --certificate-oidc-issuer … <IMAGE>@sha256:…`
   Verification checks the signature and the identity — it does not check that the predicate content
   is true.

4. **Read it back.** `cosign download attestation <IMAGE>` returns the attestation bundle; pipe it
   through a JSON tool to extract the predicate. `cosign tree <IMAGE>` shows everything attached.

5. **Gate on it.** Apply your own policy to the decoded predicate. Cosign verifies provenance; it
   does not decide whether an SBOM is acceptable.

## Reversal
`cosign clean --type attestation <IMAGE>` removes the registry-side attestation. The transparency-log
entry is permanent. See `conventions/cosign-conventions.yml`.

## Error handling
Branch on the exit code, never on STDERR text — see `errors/cosign-error-codes.yml`.
