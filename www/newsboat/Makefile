COMMENT =	RSS/Atom feed reader for text terminals

V =		2.40
DISTNAME =	newsboat-$V

CATEGORIES =	www

HOMEPAGE =	https://newsboat.org/

MAINTAINER =	Frederic Cambus <fcambus@openbsd.org>

# MIT
PERMIT_PACKAGE =	Yes

WANTLIB +=	${COMPILER_LIBCXX} ${MODCARGO_WANTLIB} crypto curl curses iconv intl
WANTLIB +=	json-c m sqlite3 ssl stfl xml2

SITES =		https://newsboat.org/releases/$V/

EXTRACT_SUFX =	.tar.xz

COMPILER =	base-clang ports-gcc

DISTFILES +=	${DISTNAME}${EXTRACT_SUFX}
MODULES =	devel/cargo

MODCARGO_BUILD =	No
MODCARGO_INSTALL =	No
MODCARGO_TEST =		No

BUILD_DEPENDS =	devel/gettext,-tools \
		misc/findutils \
		textproc/asciidoctor

RUN_DEPENDS =	x11/gtk+4,-guic

LIB_DEPENDS =	databases/sqlite3 \
		devel/gettext,-runtime \
		devel/stfl \
		devel/json-c \
		textproc/libxml \
		net/curl

MAKE_ENV =	${MODCARGO_ENV} \
		CXX="${CXX}" \
		CXXFLAGS="${CXXFLAGS}"
FAKE_FLAGS =	mandir="${PREFIX}/man"

USE_GMAKE =	Yes

ALL_TARGET =	all doc

CONFIGURE_STYLE = cargo simple
CONFIGURE_SCRIPT = config.sh

pre-configure:
	@ln -fs /usr/local/bin/gfind ${WRKDIR}/bin/find
	@sed -i 's,-Werror ,,g' ${WRKSRC}/Makefile

.include "crates.inc"

.include <bsd.port.mk>
