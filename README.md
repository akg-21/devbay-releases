# devbay

A local web development environment for **Windows and Linux**, a modern
replacement for XAMPP. One command sets up Apache or nginx, PHP (several
versions side by side), MariaDB and phpMyAdmin. devbay then creates your
projects with a local URL (`https://shop.test`), a trusted HTTPS certificate,
a database and the hosts file entry.

- Apache or nginx, PHP 8.x (one version per project), MariaDB, phpMyAdmin
- Optional: Redis, PostgreSQL, Memcached, Mailpit (catches outgoing mail), Adminer
- Trusted local HTTPS with no browser warnings
- Clone a git repo and set it up in one step, including Node, Python, Go and other apps
- Share a project with your phone on the same Wi-Fi (`devbay lan shop on`)
- Safe by default: everything is local only, and downloads are checksum-verified

## Download

Get the latest version from the **[Releases](https://github.com/akg-21/devbay-releases/releases/latest)** page:

| System | File |
|---|---|
| Windows 10/11 (64-bit) | `devbay-windows-amd64.exe` |
| Linux x86-64 | `devbay-linux-amd64` |
| Linux ARM64 (Raspberry Pi 4/5, ARM servers) | `devbay-linux-arm64` |

`SHA256SUMS.txt` lists each file's checksum.

## Install

### Windows (PowerShell)

```powershell
New-Item -ItemType Directory -Force "$env:LOCALAPPDATA\devbay" | Out-Null
Invoke-WebRequest https://github.com/akg-21/devbay-releases/releases/latest/download/devbay-windows-amd64.exe -OutFile "$env:LOCALAPPDATA\devbay\devbay.exe"
[Environment]::SetEnvironmentVariable("Path", [Environment]::GetEnvironmentVariable("Path", "User") + ";$env:LOCALAPPDATA\devbay", "User")
```

Open a new terminal (Command Prompt, PowerShell or Windows Terminal) and run
`devbay version`.

Windows may show "Windows protected your PC" the first time. Click
**More info**, then **Run anyway**.

### Linux

```sh
sudo curl -fL -o /usr/local/bin/devbay https://github.com/akg-21/devbay-releases/releases/latest/download/devbay-linux-amd64
sudo chmod +x /usr/local/bin/devbay
devbay version
```

On ARM, use `devbay-linux-arm64` instead.

## Quick start

```sh
devbay stack install      # pick the components; sensible defaults are pre-selected
devbay start
devbay new                # asks for a name, URL, HTTPS and a database
devbay list
devbay doctor             # checks everything, including the security settings
```

Clone an existing project:

```sh
devbay clone https://github.com/you/shop.git --branch develop
```

Other useful commands:

```sh
devbay https shop on      # trusted https://shop.test
devbay lan shop on        # open it from your phone on the same Wi-Fi
devbay stack add redis    # add Redis, PostgreSQL, Memcached, Mailpit or Adminer later
devbay stack web nginx    # switch between Apache and nginx
devbay php install 8.2    # another PHP version, per project
devbay help
```

## Uninstall

```sh
devbay uninstall          # removes sites, hosts entries, the CA and the firewall rule
devbay uninstall --purge  # also removes devbay's settings and saved passwords
```

Then delete `devbay.exe` (Windows) or `/usr/local/bin/devbay` (Linux). Your
project folders and databases are never deleted.

## License

devbay is free to use. See [LICENSE.txt](LICENSE.txt) and
[THIRD_PARTY_LICENSES.txt](THIRD_PARTY_LICENSES.txt).
