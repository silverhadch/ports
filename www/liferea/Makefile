COMMENT=	simple GTK desktop news aggregator

V=		1.14.6
DISTNAME=	liferea-${V}
REVISION=	5

CATEGORIES=	www news x11

HOMEPAGE=	https://lzone.de/liferea/

# GPLv2+
PERMIT_PACKAGE=	Yes

WANTLIB += ${COMPILER_LIBCXX}
WANTLIB += EGL GL LLVM X11 X11-xcb Xau Xcomposite Xcursor Xdamage
WANTLIB += Xdmcp Xext Xfixes Xi Xinerama Xrandr Xrender Xxf86vm
WANTLIB += aom aspell atk-1.0 atk-bridge-2.0 atspi brotlicommon
WANTLIB += brotlidec brotlienc c cairo cairo-gobject dav1d dbus-1
WANTLIB += drm elf enchant-2 epoll-shim epoxy
WANTLIB += execinfo expat ffi flite flite_cmu_grapheme_lang flite_cmu_grapheme_lex
WANTLIB += flite_cmu_indic_lang flite_cmu_indic_lex flite_cmu_time_awb
WANTLIB += flite_cmu_us_awb flite_cmu_us_kal flite_cmu_us_kal16
WANTLIB += flite_cmu_us_rms flite_cmu_us_slt flite_cmulex flite_usenglish
WANTLIB += fontconfig freetype fribidi gbm gcrypt gdk-3 gdk_pixbuf-2.0
WANTLIB += gio-2.0 girepository-1.0 glapi glib-2.0 gmodule-2.0
WANTLIB += gobject-2.0 gpg-error graphite2 gstallocators-1.0 gstapp-1.0
WANTLIB += gstaudio-1.0 gstbase-1.0 gstfft-1.0 gstgl-1.0 gstpbutils-1.0
WANTLIB += gstreamer-1.0 gsttag-1.0 gsttranscoder-1.0 gstvideo-1.0
WANTLIB += gthread-2.0 gtk-3 harfbuzz harfbuzz-icu hwy hyphen
WANTLIB += iconv icudata icui18n icuuc idn2 intl javascriptcoregtk-4.0
WANTLIB += jpeg json-glib-1.0 jxl jxl_cms lcms2 lzma m orc-0.4
WANTLIB += pango-1.0 pangocairo-1.0 pangoft2-1.0 pciaccess pcre2-8
WANTLIB += peas-1.0 peas-gtk-1.0 pixman-1 png psl secret-1 sharpyuv
WANTLIB += sndio soup-2.4 sqlite3 tasn1 unistring wayland-client
WANTLIB += wayland-cursor wayland-egl wayland-server webkit2gtk-4.0
WANTLIB += webp webpdemux webpmux woff2common woff2dec xcb xcb-dri2
WANTLIB += xcb-dri3 xcb-glx xcb-present xcb-randr xcb-render xcb-shm
WANTLIB += xcb-sync xcb-xfixes xkbcommon xml2 xshmfence xslt z

COMPILER=	base-clang ports-gcc

SITES=		https://github.com/lwindolf/liferea/releases/download/v${V}/

EXTRACT_SUFX=	.tar.bz2

MODULES=	devel/dconf \
		lang/python \
		textproc/intltool

USE_GMAKE=	Yes

BUILD_DEPENDS=	devel/gobject-introspection

LIB_DEPENDS=	devel/json-glib \
		devel/libpeas \
		textproc/enchant2 \
		www/webkitgtk4

RUN_DEPENDS=	devel/desktop-file-utils \
		x11/gtk+4,-guic

# lib/liferea/plugins/{libnotify,media-player}.py
RUN_DEPENDS +=	devel/libnotify \
		multimedia/gstreamer1/core

CONFIGURE_STYLE= gnu
CONFIGURE_ARGS=	--docdir=${PREFIX}/share/doc/liferea
CONFIGURE_ENV=	CPPFLAGS="-I${LOCALBASE}/include" \
		LDFLAGS="-L${LOCALBASE}/lib"

# https://github.com/lwindolf/liferea/issues/767
MAKE_ENV +=	WEBKIT_DISABLE_COMPOSITING_MODE=1

FAKE_FLAGS=	htmldocdir="${PREFIX}/share/doc/liferea/html"

post-install:
	rm ${PREFIX}/lib/liferea/web-extension/*.{a,la}
	${MODPY_COMPILEALL} ${PREFIX}/lib/liferea/plugins/

.include <bsd.port.mk>
