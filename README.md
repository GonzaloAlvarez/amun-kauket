# Amun Kauket

**amun-kauket** is a plugin for [amun](https://github.com/GonzaloAlvarez/amun) that installs [kauket](https://github.com/GonzaloAlvarez/kauket) across platforms.

---

## Usage

Run the kauket plugin through amun:

```bash
amun kauket
```

This installs the latest pinned kauket binary at `/usr/local/bin/kauket`, ensures the local config dir `~/.config/kauket` exists with mode `0700`, and prints the next step.

Expected output:

```text
kauket installed
next: kauket enroll --request ssh
```

## Supported Platforms

| Platform      | Method                          |
|---------------|----------------------------------|
| Debian/Ubuntu | GitHub Release binary + apt deps |
| macOS         | GitHub Release binary            |
| Arch Linux    | GitHub Release binary + pacman deps |

## Idempotence

Running `amun kauket` repeatedly is safe. If the installed version already matches the pinned `kauket_version`, the role only ensures the config dir exists and prints the version banner. It will NOT touch existing identity files under `~/.config/kauket/identities/`.

## Overriding the version

Edit `roles/kauket/defaults/main.yml` or pass via extra vars:

```bash
amun kauket -e kauket_version=1.0.0
```

## Security

The role downloads the release tarball over HTTPS and verifies its SHA-256 against `checksums.txt` published alongside the release. The download fails if the checksum does not match. Binaries are then installed to `/usr/local/bin/kauket` (requires sudo by default; set `kauket_install_become=false` and a user-writable `kauket_install_dir` to install to `~/.local/bin/`).

## Testing

```bash
./test
```

Runs Molecule against a Debian 12 Docker image.

## License

GNU GENERAL PUBLIC LICENSE
Version 3, 29 June 2007

Copyright (c) 2026 Gonzalo Alvarez
