COMMENT=	tty-based e-mail client

DISTNAME=	mutt-2.2.14
REVISION=	0
EPOCH=		3

CATEGORIES=	mail
HOMEPAGE=	http://www.mutt.org/

MAINTAINER=	Stuart Henderson <stu.ports@spacehopper.org>

# GPLv2+
PERMIT_PACKAGE=	Yes

# uses pledge()
WANTLIB+=	c crypto curses iconv idn2 intl pthread qdbm ssl unistring z

SITES=		http://ftp.mutt.org/pub/mutt/ \
		https://ftp.osuosl.org/pub/mutt/ \
		https://bitbucket.org/mutt/mutt/downloads/ \
		ftp://ftp.mutt.org/pub/mutt/

LIB_DEPENDS=	databases/qdbm \
		devel/gettext,-runtime \
		devel/libidn2
BUILD_DEPENDS+=	textproc/docbook-xsl \
		www/lynx
DEBUG_PACKAGES=	${BUILD_PACKAGES}
COMPILER=	base-clang ports-gcc
COMPILER_LANGS=	c

FLAVORS=	gpgme sasl slang
FLAVOR?=

CONFIGURE_STYLE=  gnu

FLAVOR_COMMA=	${FLAVOR_EXT:S/-/,/g}
SUBST_VARS=	FLAVOR_COMMA

MODULES=	lang/python
MODPY_RUNDEP=	No
MODPY_BUILDDEP=	No
MODPY_ADJ_FILES= contrib/markdown2html

CONFIGURE_ARGS+= --enable-compressed \
		--enable-debug \
		--enable-external_dotlock \
		--disable-fcntl \
		--enable-flock \
		--with-idn2 \
		--enable-imap \
		--enable-pop \
		--enable-sidebar \
		--enable-smtp \
		--mandir=${PREFIX}/man \
		--with-docdir="${PREFIX}/share/doc/mutt" \
		--with-ssl
# the header cache can use various db backends; kyotocabinet, tokyocabinet,
# lmdb, qdbm, gdbm, bdb. changing it will invalidate the cache which is
# painful for users with poorly performing imap servers so try to avoid it
# unless some other change invalidates the cache anyway
CONFIGURE_ARGS+= --enable-hcache \
		--with-qdbm
CONFIGURE_ENV=	CPPFLAGS="-I${LOCALBASE}/include" \
		LDFLAGS="-L${LOCALBASE}/lib" \
		ISPELL="${LOCALBASE}/bin/ispell"
SYSCONFDIR=	${BASESYSCONFDIR}/mutt
FAKE_FLAGS=	sysconfdir="${PREFIX}/share/examples/mutt"

## standard flavours:

.if ${FLAVOR:Mgpgme}
CONFIGURE_ARGS+= --enable-autocrypt \
		--enable-gpgme \
		--with-sqlite3
LIB_DEPENDS+=	databases/sqlite3 \
		security/gpgme
WANTLIB+=	assuan gpg-error gpgme sqlite3
.endif

.if ${FLAVOR:Msasl}
CONFIGURE_ARGS+= --with-sasl=${LOCALBASE}
LIB_DEPENDS+=	security/cyrus-sasl2
WANTLIB+=	sasl2
.endif

.if ${FLAVOR:Mslang}
CONFIGURE_ARGS+= --with-slang="${PREFIX}"
LIB_DEPENDS+=	devel/libslang
WANTLIB+=	m slang>=14
.else
CONFIGURE_ARGS+= --with-curses
.endif

post-install:
	mv -f ${PREFIX}/share/doc/mutt/samples/* ${PREFIX}/share/examples/mutt
	cd ${PREFIX}/share/examples/mutt; \
	    chmod +x *.sh *.p[ly] mutt_xtitle markdown2html

.include <bsd.port.mk>
