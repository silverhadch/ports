COMMENT=	finds and then operates on files

DISTNAME=	findutils-4.10.0
CATEGORIES=	misc
REVISION=	0

HOMEPAGE=	https://www.gnu.org/software/findutils/

# GPLv3+
PERMIT_PACKAGE=	Yes

WANTLIB=	c iconv intl m pthread

SITES=		${SITE_GNU:=findutils/}
EXTRACT_SUFX=	.tar.xz

LIB_DEPENDS=	devel/gettext,-runtime

CONFIGURE_STYLE= gnu
CONFIGURE_ARGS=	--program-prefix="g"
CONFIGURE_ENV=	CPPFLAGS="-I${LOCALBASE}/include" \
		LDFLAGS="-L${LOCALBASE}/lib"
# only used for testsuite
CONFIGURE_ENV+=	PYTHON=:

# test-sigusr depends on linux and errors out during build

LOCALSTATEDIR=	${BASELOCALSTATEDIR}/db

PORTHOME=	${WRKDIR}

.include <bsd.port.mk>
