# Makefile.am: Automake template for pgAdmin-installer
#
# Process this file with automake to create Makefile.in
#
BUILD_DIR := $(dir $(realpath $(lastword $(MAKEFILE_LIST))))

bin_SCRIPTS = \
	pgadmin-installer \
	resources/pgadmin-ctl \
	resources/pgadmin.desktop \
	resources/gunicorn@.service

AM_DEFAULT_SOURCE_EXT = .in

.PHONY: install uninstall reinitialize

install: $(bin_SCRIPTS)
	$(BUILD_DIR)pgadmin-installer install

uninstall: $(bin_SCRIPTS)
	$(BUILD_DIR)/pgadmin-installer uninstall

reinitialize: $(bin_SCRIPTS)
	$(BUILD_DIR)/pgadmin-installer reinitialize

clean-local:
	rm -rf $(bin_SCRIPTS)
