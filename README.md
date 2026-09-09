# Public Keys

This repository publishes JSON Web Key Sets (JWKS) used to verify JWT signatures for supported integrations and environments.

## Repository layout

Keys are organized by protocol, integration, organization, connector version, and environment:

```text
JWT/
  EPIC/
    NYU/
      strike-connector-2-5/
        prod/jwks.json
        test/jwkc.json
```

## Available keys

| Environment | JWKS file | Key ID |
| --- | --- | --- |
| Production | `JWT/EPIC/NYU/strike-connector-2-5/prod/jwks.json` | `strike-2-5-nyu-prod` |
| Test | `JWT/EPIC/NYU/strike-connector-2-5/test/jwkc.json` | `strike-2-5-nyu` |

Each file follows the JWKS format and currently contains an RSA public key for signature verification using `RS384`.

## Usage

Configure the JWT verifier with the JWKS file for the matching environment. Select the key whose `kid` matches the JWT header, and validate the token with the declared algorithm and the expected issuer, audience, and lifetime claims.

These files contain public key material only. Never commit private keys, secrets, access tokens, or certificates containing private key material.

## Updating keys

When rotating or adding a key:

1. Export only the public key as a valid JWKS document.
2. Use a unique `kid` and confirm that `use` is `sig` and `alg` is correct.
3. Keep the previous public key available during the token transition period when required.
4. Validate the JSON and test signature verification before publishing the change.