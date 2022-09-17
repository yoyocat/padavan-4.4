SRC_NAME=busybox-1.34.1

all: extract_test
	$(MAKE) -j$(HOST_NCPU) -C $(SRC_NAME)

extract_test:
	( if [ ! -d $(SRC_NAME) ]; then \
		tar -xjf $(SRC_NAME).tar.bz2; \
	fi )

clean:
	$(MAKE) -C $(SRC_NAME) distclean

romfs:
	$(MAKE) -C $(SRC_NAME) CONFIG_PREFIX=$(ROMFSDIR) install

