COMMENT=		tool to monitor interface bandwidth usage

DISTNAME=		ifstat-1.1
REVISION=		6
CATEGORIES=		net

HOMEPAGE=		http://gael.roualland.free.fr/ifstat/

# GPLv2+
PERMIT_PACKAGE=	Yes

WANTLIB=		c

SITES=			${HOMEPAGE}

CONFIGURE_STYLE=	gnu dest

NO_TEST=		Yes

FLAVORS=		snmp
FLAVOR?=

.if ${FLAVOR} == "snmp"
WANTLIB +=		netsnmp
LIB_DEPENDS=		net/net-snmp
CONFIGURE_ARGS+=	--with-snmp=${LOCALBASE}
WANTLIB+=		crypto m ssl
.else
CONFIGURE_ARGS+=	--without-snmp
.endif

.include <bsd.port.mk>
