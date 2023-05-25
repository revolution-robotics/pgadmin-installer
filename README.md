# pgAdmin for GNU/Linux desktops and servers

This script installs with user permissions a Flask-based **pgAdmin**
app hosted by **gunicorn** web server together with **GNU/Linux**
desktop suport and a systemd service. During installation, if a
*~/.pgadmin* directory does not already exist, credentials are
prompted for (and used to encrypt saved passwords) and the **pgAdmin**
(**SQLite**) database is updated accordingly.

Files installed for **GNU/Linux** desktop and systemd support include:

- [**pgAdmin**](https://www.pgadmin.org) *config_local.py* (setting, e.g.: `DATA_DIR=~/.pgadmin`),
- [**systemd**](https://systemd.io) template *${HOME}/.config/systemd/user/gunicorn@.service*,
- [**XDG**](https://www.freedesktop.org/wiki) desktop entry *${HOME}/.local/share/applications/pgadmin.desktop*, and
- command-line script `${HOME}/bin/pgadmin-ctl`.

Click on the **pgAdmin** desktop icon
![logo-32](https://github.com/revolution-robotics/pgadmin-server/assets/418762/f8a54807-2482-403f-9708-9d137bc3db2c)
to start the **pgAdmin** service and open the **pgAdmin** URL (by
default: http://localhost:5050).  Additional options are available on
the command line:

```man
Usage: pgadmin-ctl [OPTION...] enable|disable|start|stop|status|restart
Options:
  -h, --help            Print this help, then exit.
  -s, --server=ADDRESS  Set ADDRESS for pgAdmin to listen on (default: 127.0.0.1).
  -p, --port=PORT       Set PORT for pgAdmin to listen on (default: 5050).
```

# Prerequisites

- **GNU** `autoconf`
- **GNU** `make`
- `python3` and `pip3`
- [`jq`](https://github.com/stedolan/jq)

# Install **pgAdmin**

To install **pgadmin** in virtual environment, run:

```shell
git clone https://github.com/revolution-robotics.com/pgadmin-server
cd ./pgadmin-server
python -m venv ~/.local/pgadmin
source ~/.local/pgadmin/bin/activate
```

Within the virtual environment (command prompt is prefixed by *(pgadmin)*):

```shell
./autogen.sh
./configure --with-opt-path=${HOME}/.local/pgadmin/bin
gmake install
deactivate
```

# Upgrade **pgAdmin**

The virtual environment can be upgraded as follows:

```shell
/path/to/new/python -m venv --upgrade --upgrade-deps ~/.local/pgadmin/bin
```

# Remove **pgAdmin**

After installation, to remove the **pgAdmin** service and associated
files other than *~/.pgadmin* and the virtual environemnt, run:

```shell
make -C /path/to/pgadmin-server uninstall
```

To remove the virtual environment, use:

```shell
rm -rf ~/.local/pgadmin
```
