COMMENT=		modern 3D graphics API

GNOME_PROJECT=		cogl
GNOME_VERSION=		1.22.8
REVISION=		6

SHARED_LIBS +=  cogl                 3.2      # 24.3
SHARED_LIBS +=  cogl-path            0.1      # 24.3
SHARED_LIBS +=  cogl-pango           3.1      # 24.3

WANTLIB += ${COMPILER_LIBCXX} EGL X11 X11-xcb Xau Xcomposite Xdamage
WANTLIB += Xdmcp Xext Xfixes Xrandr Xrender cairo drm expat ffi
WANTLIB += fontconfig freetype fribidi gbm gdk_pixbuf-2.0 gio-2.0
WANTLIB += glapi glib-2.0 gmodule-2.0 gobject-2.0 graphite2 harfbuzz
WANTLIB += iconv intl jpeg m pango-1.0 pangocairo-1.0 pangoft2-1.0
WANTLIB += pcre2-8 pixman-1 png xcb xcb-dri3 xcb-present
WANTLIB += xcb-randr xcb-render xcb-shm xcb-sync xcb-xfixes xshmfence z
WANTLIB += LLVM drm_amdgpu elf pciaccess

DEBUG_PACKAGES =	${BUILD_PACKAGES}

MODGNOME_TOOLS +=	gobject-introspection

LIB_DEPENDS=		devel/pango \
			graphics/gdk-pixbuf2

CONFIGURE_ARGS=		--with-gl-libname=libGL.so \
			--with-gles1-libname=libGLESv1_CM \
			--with-gles2-libname=libGLESv2 \
			--enable-kms-egl-platform=yes \
			--enable-xlib-egl-platform=yes \
			--disable-maintainer-flags

TEST_DEPENDS=		shells/bash
TEST_IS_INTERACTIVE=	x11

# https://bugzilla.gnome.org/show_bug.cgi?id=726910
pre-configure:
	perl -pi -e 's,/bin/bash,${LOCALBASE}/bin/bash,' \
		${WRKSRC}/tests/run-tests.sh

.include <bsd.port.mk>
