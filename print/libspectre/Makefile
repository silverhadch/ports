# libgs from ghostscript is only provided on shared libs archs

COMMENT=	library for rendering Postscript documents

DISTNAME=	libspectre-0.2.12
REVISION=	2

CATEGORIES=	print

SHARED_LIBS +=  spectre              1.0      # 2.12

HOMEPAGE=	http://libspectre.freedesktop.org/

MAINTAINER=	Antoine Jacoutot <ajacoutot@openbsd.org>

# GPLv2
PERMIT_PACKAGE=	Yes

WANTLIB =  ${COMPILER_LIBCXX}
WANTLIB += ICE Lerc SM X11 Xext Xt avahi-client avahi-common crypto cups
WANTLIB += dbus-1 execinfo expat fontconfig freetype gs iconv idn ijs
WANTLIB += intl jbig2dec jpeg lzma m openjp2 paper png pthread ssl tiff
WANTLIB += xcb z zstd

COMPILER=	base-clang ports-gcc base-gcc

SITES=		http://libspectre.freedesktop.org/releases/

LIB_DEPENDS=	devel/gettext,-runtime \
		print/ghostscript/gnu

CONFIGURE_STYLE=gnu

CONFIGURE_ENV=	CPPFLAGS="-I${LOCALBASE}/include" \
		LDFLAGS="-L${LOCALBASE}/lib -L${X11BASE}/lib"

.ifdef DEBUG
BUILD_DEPENDS+=	graphics/cairo
CONFIGURE_ARGS+=--enable-test
.else
CONFIGURE_ARGS+=--disable-test
.endif

DEBUG_PACKAGES=	${BUILD_PACKAGES}

.include <bsd.port.mk>
