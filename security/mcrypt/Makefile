COMMENT =	extendable encryption program that supports many ciphers

DISTNAME =		mcrypt-2.6.8
REVISION =		8
CATEGORIES =		security

HOMEPAGE =		https://mcrypt.sourceforge.net/

MAINTAINER =		Benoit Lecocq <benoit@openbsd.org>

# GPLv3
PERMIT_PACKAGE =	Yes

WANTLIB =		c iconv intl ltdl mcrypt mhash pthread z

SITES =			${SITE_SOURCEFORGE:=mcrypt/}

USE_GMAKE =		Yes
LIB_DEPENDS =		security/libmcrypt \
			security/mhash \
			devel/gettext,-runtime \
			devel/libtool,-ltdl

CONFIGURE_STYLE =	gnu
CONFIGURE_ARGS += 	--enable-static --with-catgets 
CONFIGURE_ENV +=  	CPPFLAGS="-I${LOCALBASE}/include" \
                	LDFLAGS="-L${LOCALBASE}/lib -lintl -liconv -lltdl"

.include <bsd.port.mk>
