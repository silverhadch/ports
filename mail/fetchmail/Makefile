COMMENT=	mail retrieval utility for POP2, POP3, KPOP, IMAP and more

DISTNAME=	fetchmail-6.4.39
EXTRACT_SUFX=	.tar.xz
REVISION=	0

CATEGORIES=	mail
SITES=		${SITE_SOURCEFORGE:=fetchmail/}

HOMEPAGE=	https://www.fetchmail.info/

# GPLv2+
PERMIT_PACKAGE=	Yes

WANTLIB =  c crypto iconv intl pthread ssl

MODULES=		lang/python

# used for fetchmailconf only (which has a wrapper telling people to install
# python if necessary); don't force it
MODPY_RUNDEP=		No

MODPY_ADJ_FILES=	fetchmailconf.py
SUBST_VARS+=		MODPY_LIBDIR
BUILD_DEPENDS=		devel/bison
LIB_DEPENDS=		devel/gettext,-runtime

CONFIGURE_STYLE=	gnu
SEPARATE_BUILD=		Yes
CFLAGS +=		-I${LOCALBASE}/include
PORTHOME=		${WRKDIR}
CONFIGURE_ENV=		PYTHON=: YACC="bison -y"
CONFIGURE_ARGS=		--with-ssl \
			--enable-NTLM

USE_GROFF=		Yes# uses www.tmac for .URL tags

DOCS=			FAQ NOTES FEATURES README COPYING fetchmail-FAQ.html \
			fetchmail-features.html design-notes.html todo.html

# Remove those so they get rebuilt.
post-extract:
	rm ${WRKSRC}/rcfile_y.[ch]

pre-patch:
	${SUBST_CMD} -m 555 -c ${FILESDIR}/fetchmailconf ${WRKDIR}/fetchmailconf
	@tbl ${WRKSRC}/fetchmail.man > ${WRKSRC}/fetchmail.tbl && \
		cp -f ${WRKSRC}/fetchmail.tbl ${WRKSRC}/fetchmail.man

post-install:
	${INSTALL_DATA_DIR} ${PREFIX}/share/doc/fetchmail
	@cd ${PREFIX}/man/man1 && ln -sf fetchmail.1 fetchmailconf.1
	cd ${WRKSRC} && ${INSTALL_DATA} ${DOCS} ${PREFIX}/share/doc/fetchmail
	${INSTALL_SCRIPT} ${WRKSRC}/fetchmailconf.py \
		${PREFIX}/libexec/fetchmailconf.bin
	${INSTALL_SCRIPT} ${WRKDIR}/fetchmailconf ${PREFIX}/bin

.include <bsd.port.mk>
