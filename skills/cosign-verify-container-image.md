---
generated: '2026-09-07'
method: generated
name: Verify a container image signature
description: >-
  Check that a container image was signed by a specific identity — keyless or with a key — and read
  the exit code correctly instead of parsing text.
api: cli/cosign-cli.yml
operations: [cosign verify, cosign tree, cosign version]
source: >-
  Grounded in the published CLI reference at https://github.com/sigstore/cosign/tree/main/doc —
  every command and flag below was verified in doc/cosign_verify.md, doc/cosign_tree.md and
  doc/cosign_exit_codes.md. Cosign publishes no OpenAPI; the CLI is the contract.
---

# Verify a container image signature

Read-only. Nothing in this skill writes to a registry or to the transparency log.

## Auth
- Verification needs no Sigstore credential. It may need **registry** credentials to read the image
  and its attached signatures — run `cosign login`, or rely on the ambient Docker credential store.
- See `authentication/cosign-authentication.yml`.

## Steps

1. **Confirm the tool version.** `cosign version --json` prints
   `{gitVersion, gitCommit, gitTreeState, buildDate, goVersion, compiler, platform}`. The v3 and v2
   lines are both maintained; behaviour differs between majors, so record which one you are on.

2. **See what is attached (optional but cheap).** `cosign tree <IMAGE>` lists the signatures,
   attestations and SBOMs present for the reference. Use it to distinguish "nothing is signed" from
   "signed by someone else" before you run a verification that will fail.

3. **Verify keyless.** You MUST constrain both the identity and the issuer — cosign will not verify
   a keyless signature against "any identity":

   ```
   cosign verify \
     --certificate-identity-regexp '<identity or regexp>' \
     --certificate-oidc-issuer '<https://issuer>' \
     <IMAGE>
   ```

   For a key-based signature use `cosign verify --key <cosign.pub> <IMAGE>` instead.

4. **Read the exit code, not the prose.** STDERR is explicitly informational and is NOT covered by
   the Cosign versioning policy — never branch on its text. Branch on the exit code
   (`errors/cosign-error-codes.yml`):

   | Code | Meaning |
   |---|---|
   | 0 | Verified |
   | 10 | No signature on the image |
   | 11 | Non-existent tag |
   | 12 | Signatures exist, none matches your constraints |
   | 13 | No certificate found on the signature |

   The docs note these codes "may be subject to change" — pin your cosign version in CI.

## Gotchas
- A verification that passes says the artifact was signed by that identity. It says nothing about
  whether that identity should be trusted; that decision is yours.
- Verifying by tag is a moving target. Pin to a digest (`<IMAGE>@sha256:…`) when the answer matters.
