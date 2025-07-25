COMMENT =	rsync for cloud storage

V =		1.70.3
DISTNAME =	rclone-v${V}
PKGNAME =	rclone-${V}

CATEGORIES =	sysutils

HOMEPAGE =	https://rclone.org/

MAINTAINER =	Bjorn Ketelaars <bket@openbsd.org>

# MIT
PERMIT_PACKAGE =	Yes

WANTLIB =	c pthread

SITES =		https://downloads.rclone.org/v${V}/
DISTFILES =	${DISTNAME}${EXTRACT_SUFX} \
		${DISTNAME}-vendor${EXTRACT_SUFX}

MODULES =	lang/go

NO_TEST =	Yes

ALL_TARGET =	github.com/rclone/rclone

post-extract:
	mv ${WRKDIR}/vendor ${WRKDIST}

post-build:
.for s in bash fish zsh
	cd ${MODGO_WORKSPACE}/bin && \
		HOME=${WRKSRC} ./rclone genautocomplete $s rclone.$s
.endfor

do-install:
	${INSTALL_PROGRAM} ${MODGO_WORKSPACE}/bin/rclone ${PREFIX}/bin/
	${INSTALL_MAN} ${WRKSRC}/rclone.1 ${PREFIX}/man/man1
	${INSTALL_DATA_DIR} ${PREFIX}/share/bash-completion/completions/ \
		${PREFIX}/share/fish/vendor_completions.d/ \
		${PREFIX}/share/zsh/site-functions/
	${INSTALL_DATA} ${MODGO_WORKSPACE}/bin/rclone.bash \
		${PREFIX}/share/bash-completion/completions/rclone
	${INSTALL_DATA} ${MODGO_WORKSPACE}/bin/rclone.fish \
		${PREFIX}/share/fish/vendor_completions.d/
	${INSTALL_DATA} ${MODGO_WORKSPACE}/bin/rclone.zsh \
		${PREFIX}/share/zsh/site-functions/_rclone

.include <bsd.port.mk>
