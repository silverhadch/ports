COMMENT =		Timeweb Cloud CLI
V =			2.13.1
DISTNAME =		twc_cli-${V}
PKGNAME =		${DISTNAME:S/_cli//}
CATEGORIES =		sysutils net

# MIT
PERMIT_PACKAGE =	Yes

SITES =			https://github.com/timeweb-cloud/twc/releases/download/v${V}/
HOMEPAGE =		https://timeweb.cloud/docs/twc-cli

MAINTAINER =		Klemens Nanni <kn@openbsd.org>

MODULES =		lang/python
MODPY_PYBUILD =		poetry-core

RUN_DEPENDS =		devel/py-colorama \
			devel/py-shellingham \
			devel/py-typer \
			textproc/py-pygments \
			textproc/py-toml \
			textproc/py-yaml \
			www/py-requests

SUBST_VARS =		DISTNAME

.include <bsd.port.mk>
