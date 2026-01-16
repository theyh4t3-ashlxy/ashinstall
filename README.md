# Arch Installer

<div align="center">
<img src="[https://github.com/archlinux/archinstall/raw/master/docs/logo.png](https://github.com/archlinux/archinstall/raw/master/docs/logo.png)" alt="Archinstall Logo" width="200"/>

**A guided/automated Arch Linux installer and Python library.**

</div>

`archinstall` is a guided installer that follows the [Arch Linux Principles](https://wiki.archlinux.org/index.php/Arch_Linux#Principles). It also functions as a powerful **Python library** to manage services, packages, and system configurations—usually from a live medium or an existing installation.

---

## 💬 Community & Support

* **Discord:** [Join our server](https://discord.gg/aDeMffrxNg)
* **Matrix:** [#archinstall:matrix.org](https://matrix.to/#/#archinstall:matrix.org)
* **IRC:** [#archinstall@irc.libera.chat:6697](https://web.libera.chat/?channel=#archinstall)
* **Docs:** [Official Documentation](https://archinstall.archlinux.page/)

---

## 🚀 Getting Started

### 1. Installation

> [!TIP]
> You are `root` by default on the Arch ISO. If running from an existing system, use `sudo`.

| Method | Command |
| --- | --- |
| **Official ISO (Pre-installed)** | `archinstall` |
| **Pacman (Latest Release)** | `pacman -Sy archinstall` |
| **Pip (Edge)** | `pip install --upgrade archinstall` |
| **Git (Development)** | `git clone https://github.com/archlinux/archinstall` |

### 2. Running the Installer

To start the **guided** menu:

```shell
archinstall

```

To run a **declarative** installation (using JSON):

```shell
archinstall --config user_configuration.json --creds user_credentials.json

```

*Note: You can auto-generate these files by completing the guided menu and selecting **Save configuration**.*

---

## 🔧 Advanced Usage

### Scripting Your Own Install

You can use `archinstall` as a library to build custom, automated deployment scripts.

* [Interactive Script Example](https://github.com/archlinux/archinstall/blob/master/archinstall/scripts/guided.py)
* [Fully Automated Script Example](https://github.com/archlinux/archinstall/blob/master/examples/full_automated_installation.py)

### Credentials & Encryption

By default, user account passwords are hashed with `yescrypt`. Disk encryption passwords, however, must be handled specifically:

* **Plaintext:** Stored in `user_credentials.json` (Default).
* **Encrypted:** You can encrypt the credentials file itself when saving. To decrypt during install, use the `--creds-decryption-key` flag or set the `ARCHINSTALL_CREDS_DECRYPTION_KEY` environment variable.

---

## 🌍 Localization & Fonts

The installer supports multiple languages, but the Arch ISO does not include all necessary fonts.

* **Issue:** Non-Latin characters (e.g., Cyrillic, Greek) may appear as boxes.
* **Fix:** Set a compatible font manually before running the installer:
```shell
setfont LatGrkCyr-8x16

```



---

## 🛠 Testing & Development

### Testing on a Live ISO

If you need to test a specific branch while on the ISO:

1. Uninstall the pre-installed version: `pip uninstall --break-system-packages archinstall`
2. Clone and run:
```shell
git clone https://github.com/archlinux/archinstall
cd archinstall
python -m archinstall

```



### Testing via QEMU

```bash
qemu-system-x86_64 -enable-kvm -m 4096 -cpu host \
-drive if=pflash,format=raw,readonly,file=/usr/share/ovmf/x64/OVMF.4m.fd \
-drive file=./archlinux-iso-name.iso,format=raw

```

---

## ❓ FAQ

**Keyring is out of date?**
If you encounter signature errors, update the keyring first:
`pacman -Sy archlinux-keyring`

**How do I dual boot with Windows?**

1. Create unallocated space in Windows.
2. In `archinstall`, choose **Manual Partitioning**.
3. Create a new partition in the free space for `/`.
4. Assign the existing Windows **EFI partition** (ESP) to `/boot`.

---

## 🤝 Contributing

Contributions are welcome! Please read our [CONTRIBUTING.md](https://github.com/archlinux/archinstall/blob/master/CONTRIBUTING.md) to get started with bug reports, feature requests, or translations.

**Would you like me to refine the "Advanced" command section into a more detailed table of CLI flags?**
