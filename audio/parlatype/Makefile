V =		1.5.6
COMMENT =	minimal audio player for manual speech transcription
DISTNAME =	parlatype-${V}
CATEGORIES =	audio x11
REVISION =	7

SHARED_LIBS +=	parlatype                 0.0 # 1.6

HOMEPAGE =	https://gkarsay.github.io/parlatype/
MAINTAINER =	Brian Callahan <bcallah@openbsd.org>

# GPLv3+
PERMIT_PACKAGE =	Yes

WANTLIB += X11 Xcomposite Xcursor Xdamage Xext Xfixes Xi Xinerama Xrandr
WANTLIB += Xrender atk-1.0 atk-bridge-2.0 c cairo cairo-gobject epoxy
WANTLIB += expat ffi fontconfig freetype fribidi gdk-3 gdk_pixbuf-2.0
WANTLIB += gio-2.0 glib-2.0 gmodule-2.0 gobject-2.0 graphite2
WANTLIB += gstaudio-1.0 gstbase-1.0 gstreamer-1.0 gsttag-1.0
WANTLIB += gtk-3 harfbuzz iconv intl m orc-0.4 pango-1.0 pangocairo-1.0
WANTLIB += pangoft2-1.0 pcre2-8 pixman-1 png pthread xcb xcb-render xcb-shm
WANTLIB += z Xau Xdmcp ${COMPILER_LIBCXX} execinfo jpeg
WANTLIB += atspi dbus-1 epoll-shim wayland-client wayland-cursor
WANTLIB += wayland-egl xkbcommon

SITES =		https://github.com/gkarsay/parlatype/releases/download/v${V}/

MODULES =	devel/dconf \
		textproc/intltool \
		x11/gnome

MODGNOME_TOOLS=	desktop-file-utils gobject-introspection \
		gtk-update-icon-cache yelp

LIB_DEPENDS =	multimedia/gstreamer1/plugins-base \
		x11/gtk+3

RUN_DEPENDS =	multimedia/gstreamer1/plugins-good

CONFIGURE_STYLE =	gnu
CONFIGURE_ARGS =	--without-libreoffice

USE_GMAKE =	Yes

.include <bsd.port.mk>
