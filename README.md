# Stage354: Signature Key Rotation Ledger Layer

Stage354 adds a transparent signature key lifecycle and rotation ledger on top of Stage353.

This stage introduces:

- Signature key lifecycle recording
- Key rotation policy initialization
- Stage178 Assumption / Threat Model / Guarantee binding
- Ledger chaining with previous_hash and entry_hash
- GPG metadata support
- Sigstore OIDC metadata support
- Ed25519 metadata support
- PQC ML-DSA intent metadata support
- Verification-safe public key status records

This stage does not publish:

- Private keys
- Raw secret material
- Seed values
- Real PQC private key material
- Fake active PQC key claims
- Fake external transparency claims

---

## Stage353 → Stage354

Stage353 focused on:

- Verification transparency
- Verification result chaining
- Hash-linked audit history

Stage354 extends this by tracking:

- Key validity
- Key rotation
- Key revocation
- Key lifecycle state
- PQC migration readiness

---

## Stage178 Binding

Stage354 embeds the Stage178 framework:

### Assumption

- Signing keys are not assumed to remain secure forever.
- Keys may be rotated, revoked, replaced, or superseded.
- Verification must consider key validity at signing time.

### Threat Model

- Compromised keys
- Revoked key misuse
- Silent key replacement
- Future PQC algorithm migration

### Guarantee

- Transparent key lifecycle records
- Rotation history visibility
- Verification-aware key status checking
- No publication of private keys

---

## Key Lifecycle States

Supported status examples:

- active
- rotated
- revoked
- expired
- superseded
- intent_only
- not_configured

---

## Ledger Structure

Generated files:

docs/keys/stage354_key_rotation_ledger.json

docs/keys/stage354_key_rotation_result.json

docs/keys/stage354_key_rotation_summary.txt

---

## Verification Checks

Stage354 verifies:

- Stage353 result availability
- Stage178 binding presence
- Key record availability
- No private key publication
- No fake rotation claims
- No fake active PQC key claims
- Ledger chain integrity

---

## Current Decision

Current initialization result:

accept_policy_initialization

Meaning:

- Key lifecycle policy initialized
- Ledger chain established
- No active production key rotation claimed
- No private key exposure detected

---

## Safety Boundary

Stage354 is a metadata verification layer.

It does not:

- Manage production private keys
- Generate cryptographic keys
- Publish secrets
- Perform real-world key rotation
- Claim external transparency inclusion

---

## Relationship to QSP / VEP

Stage354 strengthens long-term trust verification by adding:

Evidence
↓
Verification
↓
Transparency
↓
Signature Context
↓
Key Lifecycle Tracking

This allows future verification decisions to consider:

- Was the signing key valid?
- Was the key revoked?
- Was the signature created before revocation?
- Is the signing algorithm still trusted?

---

## License

MIT License

