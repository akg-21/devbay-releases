# Nampix

A local web development environment for **Windows and Linux**, a modern
replacement for XAMPP. One command sets up Apache or nginx, PHP (several
versions side by side), MariaDB and phpMyAdmin. nampix then creates your
projects with a local URL (`https://shop.test`), a trusted HTTPS certificate,
a database and the hosts file entry.

- Apache or nginx, PHP 8.x (one version per project), MariaDB, phpMyAdmin
- Optional: Redis, PostgreSQL, Memcached, Mailpit (catches outgoing mail), Adminer
- Trusted local HTTPS with no browser warnings
- Clone a git repo and set it up in one step, including Node, Python, Go and other apps
- Share a project with your phone on the same Wi-Fi (`nampix lan shop on`)
- Safe by default: everything is local only, and downloads are checksum-verified

## Download

Get the latest version from the **[Releases](https://github.com/akg-21/devbay-releases/releases/latest)** page:

| System | File |
|---|---|
| Windows 10/11 (64-bit) | `nampix-windows-amd64.exe` |
| Linux x86-64 | `nampix-linux-amd64` |
| Linux ARM64 (Raspberry Pi 4/5, ARM servers) | `nampix-linux-arm64` |

`SHA256SUMS.txt` lists each file's checksum.

## Install

### Windows (PowerShell)

```powershell
New-Item -ItemType Directory -Force "$env:LOCALAPPDATA\nampix" | Out-Null
Invoke-WebRequest https://github.com/akg-21/devbay-releases/releases/latest/download/nampix-windows-amd64.exe -OutFile "$env:LOCALAPPDATA\nampix\nampix.exe"
[Environment]::SetEnvironmentVariable("Path", [Environment]::GetEnvironmentVariable("Path", "User") + ";$env:LOCALAPPDATA\nampix", "User")
```

Open a new terminal (Command Prompt, PowerShell or Windows Terminal) and run
`nampix version`.

Windows may show "Windows protected your PC" the first time. Click
**More info**, then **Run anyway**.

### Linux

```sh
sudo curl -fL -o /usr/local/bin/nampix https://github.com/akg-21/devbay-releases/releases/latest/download/nampix-linux-amd64
sudo chmod +x /usr/local/bin/nampix
nampix version
```

On ARM, use `nampix-linux-arm64` instead.

## Upgrading from Devbay

Nampix was called Devbay before. Install `nampix` as above, then delete the
old `devbay.exe` (and its folder `%LOCALAPPDATA%\devbay` if it only held
the program) or `/usr/local/bin/devbay`. Do not delete
`%LOCALAPPDATA%\devbay\stack` if it is there: that is your installed web
stack, and Nampix keeps using it. The first `nampix` run moves your settings
over, and your projects, databases and certificates keep working.

## Quick start

```sh
nampix stack install      # pick the components; sensible defaults are pre-selected
nampix start
nampix new                # asks for a name, URL, HTTPS and a database
nampix list
nampix doctor             # checks everything, including the security settings
```

Clone an existing project:

```sh
nampix clone https://github.com/you/shop.git --branch develop
```

Other useful commands:

```sh
nampix https shop on      # trusted https://shop.test
nampix lan shop on        # open it from your phone on the same Wi-Fi
nampix stack add redis    # add Redis, PostgreSQL, Memcached, Mailpit or Adminer later
nampix stack web nginx    # switch between Apache and nginx
nampix php install 8.2    # another PHP version, per project
nampix help
```

## Uninstall

```sh
nampix uninstall          # removes sites, hosts entries, the CA and the firewall rule
nampix uninstall --purge  # also removes nampix's settings and saved passwords
```

Then delete `nampix.exe` (Windows) or `/usr/local/bin/nampix` (Linux). Your
project folders and databases are never deleted.

## License

nampix is free to use. See [LICENSE.txt](LICENSE.txt) and
[THIRD_PARTY_LICENSES.txt](THIRD_PARTY_LICENSES.txt).
