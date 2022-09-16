SRC_NAME=nmap-7.93

CFLAGS += -DOPENSSL_API_COMPAT=0x10100000L

all: extract_test config_test
	$(MAKE) -j$(HOST_NCPU) -C $(SRC_NAME)

extract_test:
	( if [ ! -d $(SRC_NAME) ]; then \
		tar -xjf $(SRC_NAME).tar.bz2; \
	fi )

config_test:
	( if [ -f ./config_done ]; then \
		echo "the same configuration"; \
	else \
		make configure && touch config_done; \
	fi )

configure:
	( cd $(SRC_NAME) ; \
	./configure \
		--prefix=/usr \
		--disable-nls \
		--without-libssh2 \
		--without-ndiff \
		--without-zenmap \
		--without-nping \
		--without-liblua \
		--with-libpcap=$(STAGEDIR) \
		--with-openssl=$(STAGEDIR) \
		--with-libz=$(STAGEDIR) \
		--host=$(HOST_TARGET) \
		--build=$(HOST_BUILD) ; \
	)

clean:
	if [ -f $(SRC_NAME)/Makefile ] ; then \
		$(MAKE) -C $(SRC_NAME) distclean ; \
	fi ; \
	rm -f ncat
	rm -f config_done

romfs:
	cp $(SRC_NAME)/ncat/ncat .
	$(STRIP) ncat
	$(ROMFSINST) /usr/bin/ncat
