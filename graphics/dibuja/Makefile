V =		0.24.0
REVISION =	0
COMMENT =	simple to use paint program
DISTNAME =	dibuja-${V}
CATEGORIES =	graphics x11

HOMEPAGE =	https://launchpad.net/dibuja
MAINTAINER =	Brian Callahan <bcallah@openbsd.org>

# GPLv3+
PERMIT_PACKAGE =	Yes

WANTLIB += ${COMPILER_LIBCXX} X11 Xau Xcomposite Xcursor Xdamage
WANTLIB += Xdmcp Xext Xfixes Xi Xinerama Xrandr Xrender atk-1.0
WANTLIB += babl-0.1 brotlicommon brotlidec c cairo exiv2 expat
WANTLIB += ffi fontconfig freetype fribidi gdk-x11-2.0 gdk_pixbuf-2.0
WANTLIB += gegl-0.4 gexiv2 gio-2.0 glib-2.0 gmodule-2.0 gobject-2.0
WANTLIB += graphite2 gtk-x11-2.0 harfbuzz iconv intl jpeg json-glib-1.0
WANTLIB += lcms2 m pango-1.0 pangocairo-1.0 pangoft2-1.0 pcre2-8
WANTLIB += pixman-1 png xcb xcb-render xcb-shm z
WANTLIB += INIReader crypto curl inih nghttp2 nghttp3 ngtcp2 ngtcp2_crypto_quictls
WANTLIB += ssl

SITES =		https://launchpad.net/dibuja/trunk/${V}/+download/

COMPILER =	base-clang ports-gcc

MODULES =	textproc/intltool

BUILD_DEPENDS =	devel/gettext,-tools

LIB_DEPENDS =	graphics/gegl04 \
		graphics/libgexiv2 \
		x11/gtk+2

RUN_DEPENDS =	devel/desktop-file-utils

CONFIGURE_STYLE =	gnu
CONFIGURE_ARGS =	--libdir="${LOCALBASE}/lib"

USE_GMAKE =	Yes

.include <bsd.port.mk>
