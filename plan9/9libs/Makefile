# varargs misuse, and unportable software
ONLY_FOR_ARCHS= 	i386 sparc64

COMMENT=		Plan 9 compatibility libraries

DISTNAME=		9libs-1.0
REVISION=		11
CATEGORIES=		plan9 devel
SHARED_LIBS=		Xg	0.0 \
			frame	0.0 \
			plan9c	0.0
MODGNU_SHARED_LIBS=	Xg	'' \
			frame	'' \
			plan9c	''

HOMEPAGE=		https://netlib.org/research/9libs/

# BSD licence
PERMIT_PACKAGE=	Yes

WANTLIB =  ICE SM X11 Xau Xdmcp Xt m pthread xcb

SITES=			${HOMEPAGE}

SEPARATE_BUILD=		Yes
USE_GMAKE=		Yes
CONFIGURE_STYLE=	gnu

CONFIGURE_ARGS+=        --includedir=${PREFIX}/include/9libs

# broken on colorinit() in test.c
TEST_IS_INTERACTIVE=	Yes
SETENV=			env
TEST_TARGET=		check


.include <bsd.port.mk>
