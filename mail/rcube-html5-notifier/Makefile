COMMENT=	roundcube plugin: add HTML5 notifications for new mail

GH_ACCOUNT=	stremlau
GH_PROJECT=	html5_notifier
GH_COMMIT=	5d85947e16ea9cac4544c59666fe0ff13ba2a44a
DISTNAME=	html5_notifier-0.6.4pl20230628
PKGNAME=	rcube-${DISTNAME}

CATEGORIES=	mail www

# ISC
PERMIT_PACKAGE=	Yes

NO_BUILD=	Yes
NO_TEST=	Yes
PKG_ARCH=	*

PREFIX=		${VARBASE}/www
INSTDIR=	${PREFIX}/roundcubemail/plugins
TINSTDIR=	${TRUEPREFIX}/roundcubemail/plugins
SUBST_VARS=	INSTDIR TINSTDIR

RUN_DEPENDS=	mail/roundcubemail>=1.1

do-install:
	${INSTALL_DATA_DIR} ${INSTDIR}/html5_notifier
	cp -Rp ${WRKDIST}/* ${INSTDIR}/html5_notifier
	chown -R ${SHAREOWN}:${SHAREGRP} ${INSTDIR}

.include <bsd.port.mk>
