COMMENT=	encode, inspect, and decode Opus files

DISTNAME=	opus-tools-0.2
CATEGORIES=	audio
REVISION=	0

HOMEPAGE=	https://opus-codec.org/

MAINTAINER=	Christian Weisgerber <naddy@openbsd.org>

# GPLv2
PERMIT_PACKAGE=	Yes

SITES=		https://archive.mozilla.org/pub/opus/

LIB_DEPENDS=	audio/flac \
		audio/libogg \
		audio/libopusenc \
		audio/opus \
		audio/opusfile

WANTLIB=  FLAC c crypto m ogg opus opusenc opusfile opusurl pthread
WANTLIB+= sndio ssl

SEPARATE_BUILD=	Yes
CONFIGURE_STYLE=gnu
CONFIGURE_ARGS=	--disable-maintainer-mode

# Don't interfere with OpenBSD defaults
CONFIGURE_ARGS+=--disable-stack-protector --disable-pie

.include <bsd.port.mk>
