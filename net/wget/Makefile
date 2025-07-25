COMMENT =	retrieve files from the web via HTTP, HTTPS and FTP

DISTNAME =	wget-1.25.0
CATEGORIES =	net
REVISION =	0

HOMEPAGE =	https://www.gnu.org/software/wget/
MAINTAINER =	Nam Nguyen <namn@openbsd.org>

# GPLv3
PERMIT_PACKAGE =	Yes

WANTLIB += c crypto iconv idn2 intl pcre2-8 psl pthread ssl unistring z

BUILD_DEPENDS =		devel/gettext,-tools

LIB_DEPENDS =		converters/libunistring \
			devel/gettext,-runtime \
			devel/libidn2 \
			devel/pcre2 \
			net/libpsl

SITES =			${SITE_GNU:=wget/}

# some regression tests require python3
MODULES +=		lang/python
MODPY_RUNDEP =		No

TEST_DEPENDS =		www/p5-HTTP-Daemon ${MODPY_RUN_DEPENDS}
# Test-proxied-https-auth.px
TEST_DEPENDS +=		www/p5-HTTP-Message security/p5-IO-Socket-SSL

FAKE_FLAGS =		sysconfdir="${PREFIX}/share/examples/wget"

CONFIGURE_STYLE =	gnu
CONFIGURE_ARGS =	--with-ssl=openssl
CONFIGURE_ENV +=	CPPFLAGS="-I${LOCALBASE}/include" \
			LDFLAGS="-L${LOCALBASE}/lib"
MODGNU_CONFIG_GUESS_DIRS = ${WRKSRC}/build-aux

pre-build:
	@${SUBST_CMD} ${WRKSRC}/doc/wget.texi ${WRKSRC}/doc/sample.wgetrc

.include <bsd.port.mk>
