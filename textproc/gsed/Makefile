COMMENT=		GNU stream editor

DISTNAME=		sed-4.9
PKGNAME=		g${DISTNAME}
CATEGORIES=		textproc
SITES=			${SITE_GNU:=sed/}
EXTRACT_SUFX=		.tar.xz
REVISION=		1

HOMEPAGE=		https://www.gnu.org/software/sed/

MAINTAINER=		Armin Wolfermann <armin@wolfermann.org>

# GPLv3+
PERMIT_PACKAGE=	Yes

WANTLIB=		c iconv intl pthread

DEBUG_PACKAGES =	${BUILD_PACKAGES}

LIB_DEPENDS=		devel/gettext,-runtime
BUILD_DEPENDS=		devel/bison

CONFIGURE_STYLE=	gnu
CONFIGURE_ARGS+=	--program-prefix=g

PORTHOME =		${WRKDIR}

.include <bsd.port.mk>
