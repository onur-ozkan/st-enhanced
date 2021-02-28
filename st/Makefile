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
	sudo mkdir -p /usr/share/fonts/ibm-plex
	sudo cp -f IBMPlexMono-Medium.ttf /usr/share/fonts/ibm-plex/

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
	sudo cp ./config/.Stdefaults ~

desktop-icon:
	sudo cp -f icon.svg /usr/share/icons/default/st.svg
	sudo cp -f st.desktop /usr/share/applications

clean:
	rm -f st $(OBJ) st-$(VERSION).tar.gz *.rej *.orig *.o

dist: clean
	mkdir -p st-$(VERSION)
	cp -R FAQ LEGACY TODO LICENSE Makefile README config/config.mk\
		config/config.h st.info st.shortcuts arg.h st.h win.h $(SRC)\
		st-$(VERSION)
	tar -cf - st-$(VERSION) | gzip > st-$(VERSION).tar.gz
	rm -rf st-$(VERSION)

install: font st config-files desktop-icon
	mkdir -p $(DESTDIR)$(PREFIX)/bin
	sudo cp -f st $(DESTDIR)$(PREFIX)/bin
	sudo cp -f st-copyout $(DESTDIR)$(PREFIX)/bin
	sudo cp -f st-urlhandler $(DESTDIR)$(PREFIX)/bin
	sudo chmod 755 $(DESTDIR)$(PREFIX)/bin/st
	sudo chmod 755 $(DESTDIR)$(PREFIX)/bin/st-copyout
	sudo chmod 755 $(DESTDIR)$(PREFIX)/bin/st-urlhandler
	mkdir -p $(DESTDIR)$(MANPREFIX)/man1
	sudo sh -c "sed "s/VERSION/$(VERSION)/g" < st.shortcuts > $(DESTDIR)$(MANPREFIX)/man1/st.shortcuts"
	sudo chmod 644 $(DESTDIR)$(MANPREFIX)/man1/st.shortcuts
	tic -sx st.info
	@echo Please see the README file regarding the terminfo entry of st.

uninstall:
	sudo rm -f $(DESTDIR)$(PREFIX)/bin/st
	sudo rm -f $(DESTDIR)$(PREFIX)/bin/st-copyout
	sudo rm -f $(DESTDIR)$(PREFIX)/bin/st-urlhandler
	sudo rm -f $(DESTDIR)$(MANPREFIX)/man1/st.shortcuts
	sudo rm -f /usr/share/fonts/ibm-plex/IBMPlexMono-Medium.ttf
	sudo rm -f /usr/share/applications/st.desktop
	sudo rm -f ~/.Stdefaults
	sudo rm -f /usr/share/icons/default/st.svg

.PHONY: all options clean dist install uninstall
