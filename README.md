# Meilleur Commander: Linux Client Releases

Official **public, binary-only** distribution of Meilleur Commander Linux client artifacts, owned by [Meilleur-Tech](https://github.com/Meilleur-Tech).

## Download and install

**[Open the Linux Downloads (GitHub Releases)](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases)**

The current published release is **2.1.0**, with a **Linux GUI package for x86_64 (amd64)**. Two separately installable variants, **GUI** and **Headless**, are planned for Linux 2.2 but **are not available for download yet**. Do not treat a tarball installed with `--tray off` as a separate headless-only distribution.

**Check CPU architecture before downloading** (especially in Ubuntu inside Parallels on an Apple-Silicon Mac):

```sh
uname -m
```

- `x86_64`: supported by the currently published native Linux 2.1.0 GUI package.
- `aarch64` / `arm64`: **no native Linux ARM64 release is published yet**. Do not install or rename the x86_64 binaries. ARM64 needs a separately built, signed and tested release.

### Linux GUI 2.1.0 (x86_64)

1. Open the [2.1.0 Release](https://github.com/Meilleur-Tech/Meilleur-Commander-Linux-Releases/releases/tag/linux-client-v2.1.0) and download **`Meilleur-Commander-Client-Linux-x86_64-2.1.0.tar.gz`** from **Assets**.
2. As your normal desktop user (not root), open a terminal in the download directory and verify the actual published release asset SHA256:

   ```sh
   cd ~/Downloads
   echo '7008c72e0cccdc3dd39386f584e84bf30fa77dc710b2257698e0f0588bf767fd  Meilleur-Commander-Client-Linux-x86_64-2.1.0.tar.gz' | sha256sum -c -
   ```

3. Extract and run the **installer included in the release**. No additional shell script or source checkout is required:

   ```sh
   tar -xzf Meilleur-Commander-Client-Linux-x86_64-2.1.0.tar.gz
   cd Meilleur-Commander-Client-Linux-x86_64-2.1.0
   ./install.sh --background on --tray on
   ~/.local/bin/meilleur-commander-client
   ```

   For an **approved private/self-hosted Gateway**, select the HTTPS authority at installation time using `./install.sh --gateway https://your-gateway.example --background on --tray on`. Use the Gateway URL you were given; this parameter changes routing, **not** product entitlement. Follow the normal browser approval to enroll your device. Never share enrollment codes, tokens or private keys in an issue.

4. After installation, check the client locally with `~/.local/bin/meilleur-client status` and `~/.local/bin/meilleur-client version`. The persistent client state and enrollment are separate from replaceable app versions. **Updates are controlled by the assigned Gateway and signed release compatibility, not by selecting any newer GitHub tag.**

For Linux servers without a desktop, wait for the **separately signed Linux Headless** package in the planned 2.2 release. The existing 2.1.0 universal package can run its Core without a GUI session, but still includes the desktop GUI binary and **is not** the final headless-only customer distribution.

## Distribution and security contract

- This repository stores immutable Linux **Release** assets, not application source, signing keys, credentials, customer data or Gateway configuration.
- GitHub **Latest** is Linux-specific in this repository. It is a discovery hint, **not** permission to install, activate or downgrade a client.
- The assigned Gateway selects an exact version and validates its RSA-signed manifest, artifact hash, Bridge protocol and Gateway compatibility before activation.
- `channels/stable.json` is **untrusted discovery metadata**. The Gateway must verify the exact signed release manifest separately. A null release means nothing has yet been published here.
- Existing artifacts and immutable tags in `pmeger/Meilleur-Commander-Releases` remain valid for currently activated installations. Never mutate old URLs, signatures or release assets.

Canonical development: [Meilleur-Tech/Meilleur-Commander](https://github.com/Meilleur-Tech/Meilleur-Commander), issue [#536](https://github.com/Meilleur-Tech/Meilleur-Commander/issues/536). Linux GUI/Headless 2.2 tracking: [#1552](https://github.com/Meilleur-Tech/Meilleur-Commander/issues/1552). The release RSA authority is `mc-client-caf94007b07dc90b`; its private key stays exclusively on the Owner signing host, never on the Linux build runner or in this repository.
