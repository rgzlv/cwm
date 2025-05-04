XQUARTZ=	/opt/X11
CPPFLAGS=	-I$(XQUARTZ)/include -I/usr/local/include/freetype2 \
		-D'pledge(a, b)=0' -DHOST_NAME_MAX=1 -DYYSTYPE_IS_DECLARED
CFLAGS=		$(shell pkg-config --cflags libbsd-overlay)
LDFLAGS=	$(shell pkg-config --libs-only-L libbsd-overlay) \
		-L$(XQUARTZ)/lib
LDLIBS=		$(shell pkg-config --libs-only-l libbsd-overlay) -lXft \
		-lXrender -lX11 -lxcb -lXau -lXdmcp -lfontconfig -lexpat \
		-lfreetype -lz -lXrandr -lXext
PREFIX=		/usr/local
objs=		calmwm.o client.o conf.o group.o kbfunc.o menu.o screen.o \
		search.o util.o xevents.o xmalloc.o xutil.o parse.o

cwm: $(objs)
	$(CC) $(LDFLAGS) -o $@ $^ $(LDLIBS)

parse.o: parse.c

parse.c: parse.y
	bison -o $@ $<

install:
	mkdir -p $(PREFIX)/bin $(PREFIX)/share/man/man1 $(PREFIX)/share/man/man5
	cp cwm $(PREFIX)/bin
	cp cwm.1 $(PREFIX)/share/man/man1
	cp cwmrc.5 $(PREFIX)/share/man/man5

clean:
	rm -f cwm $(objs) parse.c
