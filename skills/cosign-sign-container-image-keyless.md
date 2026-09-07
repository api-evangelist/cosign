---
generated: '2026-09-07'
method: generated
name: Sign a container image keylessly
description: >-
  Sign an image with an OIDC identity and a short-lived Fulcio certificate, understanding that the
  transparency-log entry this creates is permanent and public.
api: cli/cosign-cli.yml
operations: [cosign sign, cosign verify, cosign tree, cosign clean]
source: >-
  Grounded in the published CLI reference at https://github.com/sigstore/cosign/tree/main/doc
  (doc/cosign_sign.md, doc/cosign_clean.md), https://docs.sigstore.dev/cosign/signing/overview/ and
  https://docs.sigstore.dev/logging/overview/ .
---

# Sign a container image keylessly

**Read this before running anything.** Keyless signing writes an entry to the Rekor transparency
log. Rekor is an append-only Merkle log: there is no delete, no redact and no expiry. The OIDC
identity in the Fulcio certificate — for an email identity, a real email address — becomes public
and permanent. If you are acting on someone's behalf, that is their identity you are publishing
irrevocably. See the `reversibility` block in `conventions/cosign-conventions.yml`.

## Auth
- An OIDC identity. In CI (GitHub Actions, GitLab, CircleCI, Codefresh and others) the token is
  picked up ambiently; interactively cosign opens a browser flow. The accepted issuers are
  enumerated live at `https://fulcio.sigstore.dev/api/v2/configuration`.
- Registry write permission for the repository the signature is stored in.

## Steps

1. **Pin the artifact.** Resolve the tag to a digest and sign the digest, not the tag:
   `<IMAGE>@sha256:…`. Signing a tag signs whatever the tag pointed at that second.

2. **Rehearse against staging first** if this is new automation. Sigstore runs a complete parallel
   deployment at `fulcio.sigstage.dev` / `rekor.sigstage.dev` / `oauth2.sigstage.dev/auth`; point
   cosign at it via `cosign initialize` against the staging TUF mirror, or with the `--fulcio-url`,
   `--rekor-url` and `--oidc-issuer` flags. See `sandbox/cosign-sandbox.yml`. Staging carries no SLO
   and is not for production use — but nothing you write there is a permanent public record of a
   real identity.

3. **Sign.** `cosign sign <IMAGE>@sha256:…`. In non-interactive automation add `-y` to skip the
   confirmation prompt only once you are certain of step 1.

4. **Verify what you just did.** `cosign verify --certificate-identity … --certificate-oidc-issuer …`
   against the same digest. A signing run that reports success but does not verify is a broken
   pipeline, not a signed artifact.

## Reversal — know it before you need it
- The registry-side signature CAN be removed: `cosign clean --type signature <IMAGE>`
  (`--type` accepts `signature | attestation | referrer | sbom | all`, default `all`; `-f` skips the
  prompt). No time window is stated; it works whenever you have registry write access.
- The transparency-log entry CANNOT be removed. Ever. `cosign clean` does not touch it.
- If a permanent public record is not acceptable for this artifact, do not sign keylessly. Use a
  key or KMS identity, or `--tlog-upload=false` — accepting that you lose the timestamping and
  third-party verifiability that keyless signing exists to provide.

## Idempotency
There is none. Re-running `cosign sign` produces a **new** signature and a **new** log entry rather
than replacing the old one; repeated invocations accumulate. Check with `cosign verify` or
`cosign tree` before signing again.
