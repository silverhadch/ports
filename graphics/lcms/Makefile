COMMENT =	color management library

DISTNAME =	lcms-1.19
CATEGORIES =	graphics
SITES =		${SITE_SOURCEFORGE:=lcms/}
REVISION =	2

SHARED_LIBS +=  lcms                 2.0      # 1.19

HOMEPAGE =	https://www.littlecms.com/

LIB_DEPENDS +=	graphics/jpeg \
		graphics/tiff

# MIT
PERMIT_PACKAGE =	Yes

WANTLIB =  ${COMPILER_LIBCXX} Lerc c jpeg lzma m pthread tiff z zstd

COMPILER =	base-clang ports-gcc base-gcc

CONFIGURE_STYLE =	gnu
CONFIGURE_ENV +=	CPPFLAGS="-I${LOCALBASE}/include" \
			LDFLAGS="-L${LOCALBASE}/lib"

post-install:
	${INSTALL_DATA_DIR} ${PREFIX}/share/doc/lcms
	${INSTALL_DATA} ${WRKSRC}/doc/* ${PREFIX}/share/doc/lcms

.include <bsd.port.mk>
