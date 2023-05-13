# configure.ac: Autoconf template for bash-dot-files.
#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.69])
AC_INIT([pgadmin_installer], [1.0.0], [])
AM_INIT_AUTOMAKE([foreign])

: ${ASDF_DIR:="${HOME}/.asdf"}

AC_ARG_VAR([ASDF_DIR], [Top-level directory of asdf version manager])
AC_MSG_CHECKING([whether to search asdf-vm path])
AC_ARG_WITH([asdf-path],
  [AS_HELP_STRING([--with-asdf-path@<:@=PATH@:>@],
    [search asdf-vm PATH @{:@default: ~/.asdf/shims@:}@])],
  [], [with_asdf_path=check])
if test ."$with_asdf_path" = .'yes' || test ."$with_asdf_path" = .'check'; then
    if test -d "$ASDF_DIR"; then
        ASDF_PREFIX=${ASDF_DIR}/shims
    else
        AC_MSG_WARN([${ASDF_DIR}: No such file or directory])
    fi
elif test ! ."$with_asdf_path" = .'no'; then
    if test -d "$with_asdf_path"; then
        ASDF_PREFIX=${with_asdf_path}
    else
        AC_MSG_WARN([${with_asdf_path}: No such file or directory])
    fi
fi
AC_MSG_RESULT([${ASDF_PREFIX:-no}])
ASDF_SHIMS_PATH=$ASDF_PREFIX
AC_SUBST([ASDF_SHIMS_PATH], ["$ASDF_SHIMS_PATH"])
ASDF_PREFIX=${ASDF_PREFIX:+"${ASDF_PREFIX}${PATH_SEPARATOR}"}

LOCAL_PREFIX=/usr/local/sbin${PATH_SEPARATOR}/usr/local/bin${PATH_SEPARATOR}

AC_MSG_CHECKING([whether to search optional path])
AC_ARG_WITH([opt-path],
  [AS_HELP_STRING([--with-opt-path@<:@=PATH@:>@],
    [search optional PATH @{:@default: /opt/local/bin@:}@])],
  [], [with_opt_path=check])
if test ."$with_opt_path" = .'yes' || test ."$with_opt_path" = .'check'; then
    if test -d /opt/local/bin; then
        OPT_PREFIX=/opt/local/sbin${PATH_SEPARATOR}/opt/local/bin
    fi
elif test ! ."$with_opt_path" = .'no'; then
    if test -d "$with_opt_path"; then
        OPT_PREFIX=${with_opt_path}
    else
        AC_MSG_WARN([${with_opt_path}: No such file or directory])
    fi
fi
AC_MSG_RESULT([${OPT_PREFIX:-no}])
OPT_PATHS=$(echo "$OPT_PREFIX" | tr "${PATH_SEPARATOR}" ' ')
AC_SUBST([OPT_PATHS], ["$OPT_PATHS"])
OPT_PREFIX=${OPT_PREFIX:+"${OPT_PREFIX}${PATH_SEPARATOR}"}

# Checks for programs.
AC_PATH_PROGS([AWK_CMD],      [gawk awk],                [], [${OPT_PREFIX}${PATH}])
AC_PATH_PROGS([CAT_CMD],      [gcat cat],                [], [${OPT_PREFIX}${PATH}])
AC_PATH_PROGS([CHMOD_CMD],    [gchmod chmod],            [], [${OPT_PREFIX}${PATH}])
AC_PATH_PROGS([GETOPT_CMD],   [ggetopt getopt],          [], [${OPT_PREFIX}${PATH}])
AC_PATH_PROGS([GREP_CMD],     [ggrep grep],              [], [${OPT_PREFIX}${PATH}])
AC_PATH_PROGS([INSTALL_CMD],  [ginstall install],        [], [${OPT_PREFIX}${PATH}])

AC_PATH_PROG([JQ_CMD],        [jq],                      [], [${OPT_PREFIX}${PATH}])

AC_PATH_PROGS([KILL_CMD],     [gkill kill],              [], [${OPT_PREFIX}${PATH}])
AC_PATH_PROGS([OPEN_CMD],     [xdg-open open],           [], [${OPT_PREFIX}${PATH}])

AC_PATH_PROG([PING_CMD],      [ping],                    [], [${OPT_PREFIX}${PATH}])
AC_PATH_PROG([PIP_CMD],       [pip3],                    [], [${OPT_PREFIX}${ASDF_PREFIX}${PATH}])
AC_PATH_PROG([PYTHON_CMD],    [python3],                 [], [${OPT_PREFIX}${ASDF_PREFIX}${PATH}])

AC_PATH_PROGS([READLINK_CMD], [greadlink readlink],      [], [${OPT_PREFIX}${PATH}])
AC_PATH_PROGS([SED_CMD],      [gsed sed],                [], [${OPT_PREFIX}${PATH}])
AC_PATH_PROGS([SLEEP_CMD],    [gsleep sleep],            [], [${OPT_PREFIX}${PATH}])
AC_PATH_PROGS([STAT_CMD],     [gstat stat],              [], [${OPT_PREFIX}${PATH}])

AC_PATH_PROG([SYSTEMCTL_CMD], [systemctl])

AC_PATH_PROGS([TAIL_CMD],     [gtail tail],              [], [${OPT_PREFIX}${PATH}])
AC_PATH_PROGS([TR_CMD],       [gtr tr],                  [], [${OPT_PREFIX}${PATH}])

AC_PATH_PROG([UPDATE_DB_CMD], [update-desktop-database])

for cmd in JQ_CMD PIP_CMD PING_CMD PYTHON_CMD SYSTEMCTL_CMD; do
    if eval test .\"\$$cmd\" = .''; then
        AC_MSG_FAILURE([$cmd: Undefined variable])
    elif eval test ! -x \"\$$cmd\"; then
        not_found_msg=$(eval echo "\$$cmd: No such command")
        AC_MSG_FAILURE([$not_found_msg])
    fi
done

if ! [python_version_major=$($PYTHON_CMD -c 'import sys; print(sys.version_info[0])')]; then
    AC_MSG_FAILURE([Python: cannot get version info])
elif test ."$python_version_major" = .'' -o $python_version_major -ne 3; then
    AC_MSG_FAILURE([Python v3 is not default Python])
fi

AC_CONFIG_FILES([
    Makefile
    resources/pgadmin.desktop
    resources/pgadmin.service
])

AC_CONFIG_FILES([pgadmin-installer], [chmod +x pgadmin-installer])
AC_CONFIG_FILES([resources/pgadmin-ctl], [chmod +x resources/pgadmin-ctl])

AC_OUTPUT
