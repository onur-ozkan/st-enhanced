# st - simple terminal
# See LICENSE file for copyright and license details.
.POSIX:

include config/config.mk

SRC = st.c x.c boxdraw/boxdraw.c harfbuzz/hb.c
OBJ = $(SRC:.c=.o)

all: options st

options:
	@echo st build options:
	@echo "CFLAGS  = $(STCFLAGS)"
	@echo "LDFLAGS = $(STLDFLAGS)"
	@echo "CC      = $(CC)"

font:
	mkdir -p /usr/share/fonts/ibm-plex
	cp -f IBMPlexMono-Medium.ttf /usr/share/fonts/ibm-plex/

.c.o:
	$(CC) $(STCFLAGS) -c $<

st.o: config/config.h st.h win.h
x.o: arg.h config/config.h st.h win.h harfbuzz/hb.h
hb.o: st.h
boxdraw.o: config/config.h st.h boxdraw/boxdraw_data.h

$(OBJ): config/config.h config/config.mk

st: $(OBJ)
	mv hb.o harfbuzz/hb.o
	mv boxdraw.o boxdraw/boxdraw.o
	$(CC) -o $@ $(OBJ) $(STLDFLAGS)

config-files:
	cp ./config/.Stdefaults /

clean:
	rm -f st $(OBJ) st-$(VERSION).tar.gz *.rej *.orig *.o

dist: clean
	mkdir -p st-$(VERSION)
	cp -R FAQ LEGACY TODO LICENSE Makefile README config/config.mk\
		config/config.h st.info st.shortcuts arg.h st.h win.h $(SRC)\
		st-$(VERSION)
	tar -cf - st-$(VERSION) | gzip > st-$(VERSION).tar.gz
	rm -rf st-$(VERSION)

install: font st config-files
	mkdir -p $(DESTDIR)$(PREFIX)/bin
	cp -f st $(DESTDIR)$(PREFIX)/bin
	cp -f st-copyout $(DESTDIR)$(PREFIX)/bin
	cp -f st-urlhandler $(DESTDIR)$(PREFIX)/bin
	chmod 755 $(DESTDIR)$(PREFIX)/bin/st
	chmod 755 $(DESTDIR)$(PREFIX)/bin/st-copyout
	chmod 755 $(DESTDIR)$(PREFIX)/bin/st-urlhandler
	mkdir -p $(DESTDIR)$(MANPREFIX)/man1
	sed "s/VERSION/$(VERSION)/g" < st.shortcuts > $(DESTDIR)$(MANPREFIX)/man1/st.shortcuts
	chmod 644 $(DESTDIR)$(MANPREFIX)/man1/st.shortcuts
	tic -sx st.info
	@echo Please see the README file regarding the terminfo entry of st.

uninstall:
	rm -f $(DESTDIR)$(PREFIX)/bin/st
	rm -f $(DESTDIR)$(PREFIX)/bin/st-copyout
	rm -f $(DESTDIR)$(PREFIX)/bin/st-urlhandler
	rm -f $(DESTDIR)$(MANPREFIX)/man1/st.shortcuts
	rm -f /usr/share/fonts/ibm-plex/IBMPlexMono-Medium.ttf
	rm -f ~/.Stdefaults

.PHONY: all options clean dist install uninstall