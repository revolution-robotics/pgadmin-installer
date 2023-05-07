# pgAdmin Installer for systemd-based GNU/Linux Desktop environments

This script installs a local **pgAdmin4** server together with **GNU/Linux**
desktop suport. During installation, the user is prompted for
credentials to encrypt saved passwords and the **pgAdmin4** (**SQLite**)
database is updated accordingly.

The files installed for **GNU/Linux** desktop support include:

- [**pgAdmin**](https://www.pgadmin.org) *config_local.py* (setting: `DATA_DIR=~/.pgadmin`),
- [**systemd**](https://systemd.io) unit file *${HOME}/.config/systemd/user/pgadmin.service*,
- [**XDG**](https://www.freedesktop.org/wiki) desktop entry *${HOME}/.local/share/applications/pgadmin.desktop*, and
- command-line script *${HOME}/bin/pgadmin-ctl*.

The `pgadmin-ctl` utility is called by *pgadmin.desktop* to start
the **pgAdmin4** service and open in the web browser the **pgAdmin4**
URL (by default: http://localhost:5050).  To stop **pgAdmin4**, in a
terminal, run:

```shell
pgadmin-ctl stop
```

# Prerequisites

- **GNU** `autoconf`
- **GNU** `make`
- `python3` and `pip3`

# Installation

To install **pgAdmin4**, run:

```shell
git clone https://github.com/revolution-robotics.com/pgadmin-installer
cd ./pgadmin-installer
./autogen.sh
./configure
gmake install
```

Verify that **pgAdmin4** is running:

```shell
pgadmin-ctl status
```

Log out and back in again to make **pgAdmin** desktop entry available
to the desktop environment - e.g., clicking on **pgAdmin** app icon should
open a web page to log into **pgAdmin**.

# Removal

After installation, to remove the **pgAdmin4** service and associated
files other than *~/.pgadmin* , run:

```shell
./pgadmin-installer uninstall
```
