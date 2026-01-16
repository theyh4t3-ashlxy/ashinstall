# arch installer

<div align="center">
<img src="[https://github.com/archlinux/archinstall/raw/master/docs/logo.png](https://github.com/archlinux/archinstall/raw/master/docs/logo.png)" alt="drawing" width="200"/>

**a guided/automated arch linux installer and python library.**

</div>

`archinstall` is a guided installer that follows the [arch linux principles](https://wiki.archlinux.org/index.php/Arch_Linux#Principles). it also functions as a powerful **python library** to manage services, packages, and system configurations—usually from a live medium or an existing installation.

---

## 💬 community & support

* **discord:** [join our server](https://discord.gg/aDeMffrxNg)
* **matrix:** [#archinstall:matrix.org](https://matrix.to/#/#archinstall:matrix.org)
* **irc:** [#archinstall@irc.libera.chat:6697](https://web.libera.chat/?channel=#archinstall)
* **docs:** [official documentation](https://archinstall.archlinux.page/)

---

## 🚀 getting started

### 1. installation

> [!TIP]
> you are `root` by default on the arch iso. if running from an existing system, use `sudo`.

| method | command |
| --- | --- |
| **official iso (pre-installed)** | `archinstall` |
| **pacman (latest release)** | `pacman -Sy archinstall` |
| **pip (edge)** | `pip install --upgrade archinstall` |
| **git (development)** | `git clone https://github.com/archlinux/archinstall` |

### 2. running the installer

to start the **guided** menu:

```shell
archinstall

```

to run a **declarative** installation (using json):

```shell
archinstall --config user_configuration.json --creds user_credentials.json

```

*note: you can auto-generate these files by completing the guided menu and selecting **save configuration**.*

---

## 🔧 advanced usage

### scripting your own install

you can use `archinstall` as a library to build custom, automated deployment scripts.

* [interactive script example](https://github.com/archlinux/archinstall/blob/master/archinstall/scripts/guided.py)
* [fully automated script example](https://github.com/archlinux/archinstall/blob/master/examples/full_automated_installation.py)

### credentials & encryption

by default, user account passwords are hashed with `yescrypt`. disk encryption passwords, however, must be handled specifically:

* **plaintext:** stored in `user_credentials.json` (default).
* **encrypted:** you can encrypt the credentials file itself when saving. to decrypt during install, use the `--creds-decryption-key` flag or set the `ARCHINSTALL_CREDS_DECRYPTION_KEY` environment variable.

---

## 🌍 localization & fonts

the installer supports multiple languages, but the arch iso does not include all necessary fonts.

* **issue:** non-latin characters (e.g., cyrillic, greek) may appear as boxes.
* **fix:** set a compatible font manually before running the installer:

```shell
setfont LatGrkCyr-8x16

```

---

## 🛠 testing & development

### testing on a live iso

if you need to test a specific branch while on the iso:

1. uninstall the pre-installed version: `pip uninstall --break-system-packages archinstall`
2. clone and run:

```shell
git clone https://github.com/archlinux/archinstall
cd archinstall
python -m archinstall

```

### testing via qemu

```bash
qemu-system-x86_64 -enable-kvm -m 4096 -cpu host \
-drive if=pflash,format=raw,readonly,file=/usr/share/ovmf/x64/OVMF.4m.fd \
-drive file=./archlinux-iso-name.iso,format=raw

```

---

## ❓ faq

**keyring is out of date?**
if you encounter signature errors, update the keyring first:
`pacman -Sy archlinux-keyring`

**how do i dual boot with windows?**

1. create unallocated space in windows.
2. in `archinstall`, choose **manual partitioning**.
3. create a new partition in the free space for `/`.
4. assign the existing windows **efi partition** (esp) to `/boot`.

---

## 🤝 contributing

contributions are welcome! please read our [contributing.md](https://github.com/archlinux/archinstall/blob/master/CONTRIBUTING.md) to get started with bug reports, feature requests, or translations.
