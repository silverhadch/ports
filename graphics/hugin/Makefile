BROKEN-hppa =	run dep on enblend-enfuse which will not build on hppa

COMMENT =	panorama image stitcher

DISTNAME =	hugin-2024.0.1
REVISION =	2

EXTRACT_SUFX =	.tar.bz2

# not needed for releases, but makes RCs/betas easier to work with
PKGNAME =	${DISTNAME:S/_//:L}
WRKDIST =	${WRKDIR}/${DISTNAME:C/_.*//}

SHARED_LIBS +=  celeste                   4.0
SHARED_LIBS +=  huginbase                 8.0
SHARED_LIBS +=  huginbasewx               7.0
SHARED_LIBS +=  icpfindlib                5.0
SHARED_LIBS +=  localfeatures             4.0
SHARED_LIBS +=  hugin_python_interface    4.0

CATEGORIES =	graphics x11

HOMEPAGE =	https://hugin.sourceforge.io/

MAINTAINER =	Kirill Bychkov <kirby@openbsd.org>

# GPLv2+
PERMIT_PACKAGE =	Yes

WANTLIB += ${COMPILER_LIBCXX} ${MODPY_WANTLIB}
WANTLIB += GL GLU Iex-3_3 IlmThread-3_3 Imath-3_1 OpenEXR-3_3 X11
WANTLIB += boost_atomic-mt boost_filesystem-mt boost_system-mt c epoxy exiv2
WANTLIB += fftw3 flann flann_cpp jpeg lcms2 lz4 m pano13 png sqlite3
WANTLIB += tiff vigraimpex wx_baseu-3.2 wx_baseu_net-3.2 wx_baseu_xml-3.2
WANTLIB += wx_gtk3u_aui-3.2 wx_gtk3u_core-3.2 wx_gtk3u_gl-3.2
WANTLIB += wx_gtk3u_html-3.2 wx_gtk3u_propgrid-3.2 wx_gtk3u_qa-3.2
WANTLIB += wx_gtk3u_xrc-3.2 z
# lensfun is dlopened, so don't remove it from WANTLIB and LIB_DEPENDS
WANTLIB += lensfun

SITES =			${SITE_SOURCEFORGE:=hugin/}

BUILD_DEPENDS =		devel/gettext,-tools \
			devel/swig>=2 \
			graphics/p5-Image-ExifTool
RUN_DEPENDS =		devel/desktop-file-utils \
			graphics/enblend-enfuse \
			graphics/p5-Image-ExifTool \
			misc/shared-mime-info \
			x11/gtk+4,-guic
RUN_DEPENDS +=		x11/py-wxPython # required for launching python scripts

LIB_DEPENDS =		devel/boost \
			graphics/exiv2>=0.12 \
			graphics/lcms2 \
			graphics/libpano13>=2.9.19 \
			graphics/lensfun \
			graphics/vigra \
			math/flann \
			x11/wxWidgets>=3.0.4

MODULES =		devel/cmake lang/python

# C++11
COMPILER =		base-clang ports-gcc

CONFIGURE_ENV =		MANDIR=man
CONFIGURE_ARGS +=	-DBUILD_HSI=ON \
			-DBUILD_WITH_EPOXY=ON \
			-Wno-dev
NO_TEST =		Yes

# Fix build with OpeEXR>=3 (Imath split)
CXXFLAGS +=		-I${LOCALBASE}/include/Imath

MODPY_ADJ_FILES =	src/hugin_script_interface/hpi.py \
			src/hugin_script_interface/plugins/shooting_pattern.py \
			src/hugin_script_interface/plugins/woa.py \
			src/hugin_script_interface/plugins/crop_cp.py \
			src/hugin_script_interface/plugins/top_five.py \
			src/hugin_script_interface/plugins-dev/dual_use.py \
			src/hugin_script_interface/plugins-dev/plugin_skeleton.py

pre-patch:
	rm ${WRKSRC}/CMakeModules/FindPNG.cmake
	rm ${WRKSRC}/CMakeModules/FindGLEW.cmake
	rm ${WRKSRC}/CMakeModules/FindZLIB.cmake
	cd ${WRKSRC}/CMakeModules; perl -i -pe 's/\r$$//' `find . -type f` \
	    ../src/CMakeLists.txt

post-install:
	${MODPY_COMPILEALL} \
		${PREFIX}/lib/python${MODPY_VERSION}/site-packages \
		${PREFIX}/share/hugin/data/plugins/

.include <bsd.port.mk>
