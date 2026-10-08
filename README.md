# Meilleur Commander: Linux Client Releases

Official **public, binary-only** distribution of Meilleur Commander Linux client artifacts, owned by [Meilleur-Tech](https://github.com/Meilleur-Tech).

- This repository stores immutable Linux **Release** assets, not application source, signing keys, credentials, customer data or Gateway configuration.
- GitHub **Latest** is Linux-specific in this repository. It is a discovery hint, **not** permission to install, activate or downgrade a client.
- The assigned Gateway selects an exact version and validates its RSA-signed manifest, artifact hash, Bridge protocol and Gateway compatibility before activation.
- `channels/stable.json` is **untrusted discovery metadata**. The Gateway must verify the exact signed release manifest separately. A null release means nothing has yet been published here.
- Existing artifacts and immutable tags in `pmeger/Meilleur-Commander-Releases` remain valid for currently activated installations. Never mutate old URLs, signatures or release assets.

Canonical development: [Meilleur-Tech/Meilleur-Commander](https://github.com/Meilleur-Tech/Meilleur-Commander), issue [#536](https://github.com/Meilleur-Tech/Meilleur-Commander/issues/536). The release RSA authority is `mc-client-caf94007b07dc90b`; its private key stays exclusively on the Owner signing host, never on the Linux build runner or in this repository.
