# XXX merge this patch and rid of the dot.la files?
# https://git.archlinux.org/svntogit/packages.git/tree/trunk/0030-dont_use_la_files_for_opening_plugins.patch?h=packages/cyrus-sasl

COMMENT=		RFC 2222 SASL (Simple Authentication and Security Layer)

V=			2.1.28
DISTNAME=		cyrus-sasl-${V}
REVISION=		2

SHARED_LIBS +=  sasl2                3.1      # 3.0
SHARED_LIBS +=	anonymous                 0.0 # 3.0
SHARED_LIBS +=	crammd5                   0.0 # 3.0
SHARED_LIBS +=	digestmd5                 0.0 # 3.0
SHARED_LIBS +=	gs2                       0.0 # 3.0
SHARED_LIBS +=	gssapiv2                  0.0 # 3.0
SHARED_LIBS +=	ldapdb                    0.0 # 3.0
SHARED_LIBS +=	login                     0.0 # 3.0
SHARED_LIBS +=	ntlm                      0.0 # 3.0
SHARED_LIBS +=	otp                       0.0 # 3.0
SHARED_LIBS +=	plain                     0.0 # 3.0
SHARED_LIBS +=	sasldb                    0.0 # 3.0
SHARED_LIBS +=	scram                     0.0 # 3.0
SHARED_LIBS +=	sql                       0.0 # 3.0

CATEGORIES=		security

HOMEPAGE=		http://www.cyrusimap.org/sasl/

MAINTAINER=		Antoine Jacoutot <ajacoutot@openbsd.org>

# see the COPYRIGHT file in package sources
PERMIT_PACKAGE=	Yes

SITES=			https://github.com/cyrusimap/cyrus-sasl/releases/download/cyrus-sasl-${V}/

WANTLIB += c crypto

COMPILER=		base-clang ports-gcc base-gcc
COMPILER_LANGS=		c

CONFIGURE_STYLE=	gnu

CONFIGURE_ENV=		CPPFLAGS="-I${LOCALBASE}/include" \
			LIBS="-L${LOCALBASE}/lib" \
			ac_cv_prog_CC_FOR_BUILD="${CC}"

CONFIGURE_ARGS=		--enable-static \
			--without-pam \
			--without-sphinx-build \
			--without-sqlite \
			--with-saslauthd="/var/sasl2" \
			--with-plugindir=${PREFIX}/lib/sasl2 \
			--enable-login \
			--enable-ntlm \
			--enable-auth-sasldb \
			--disable-sample

CFLAGS +=		-fPIC

USE_GMAKE=		Yes

FLAVORS=		db4 gssapi ldap mysql pgsql sqlite3
FLAVOR?=

.if ${FLAVOR:Mdb4}
CONFIGURE_ARGS +=	--with-dblib=berkeley \
			--with-bdb-libdir="${LOCALBASE}/lib/db4" \
			--with-bdb-incdir="${LOCALBASE}/include/db4"
LIB_DEPENDS +=		databases/db/v4
WANTLIB +=		lib/db4/db>=4
.else
CONFIGURE_ARGS +=	--with-dblib=ndbm \
			--without-bdb-libdir \
			--without-bdb-incdir
.endif

.if ${FLAVOR:Mgssapi}
CONFIGURE_ARGS +=	--enable-gssapi=${LOCALBASE}/heimdal
MODULES +=		security/heimdal
WANTLIB += execinfo
WANTLIB += heimdal/lib/gssapi
WANTLIB += heimdal/lib/heimntlm
WANTLIB += heimdal/lib/heimsqlite
.endif

.if ${FLAVOR:Mldap}
LIB_DEPENDS +=		databases/openldap
CONFIGURE_ARGS +=	--with-ldap=${LOCALBASE} \
			--enable-ldapdb
WANTLIB += lber ldap pthread ssl
.else
CONFIGURE_ARGS +=	--without-ldap
.endif

.if ${FLAVOR:Mmysql} || ${FLAVOR:Mpgsql} || ${FLAVOR:Msqlite3}
CONFIGURE_ARGS +=	--enable-sql
PKG_ARGS=		-Dsql=1
.else
CONFIGURE_ARGS +=	--disable-sql
PKG_ARGS=		-Dsql=0
.endif

.if ${FLAVOR:Mmysql}
LIB_DEPENDS +=		databases/mariadb
WANTLIB+= m mariadb pthread ssl z
CONFIGURE_ARGS +=	--with-mysql="${LOCALBASE}"
.else
CONFIGURE_ARGS +=	--without-mysql
.endif

.if ${FLAVOR:Mpgsql}
LIB_DEPENDS +=		databases/postgresql
CFLAGS +=		-I${LOCALBASE}/include/postgresql
WANTLIB += m pq pthread ssl
.else
CONFIGURE_ARGS +=	--without-pgsql
.endif

.if ${FLAVOR:Msqlite3}
LIB_DEPENDS +=		databases/sqlite3
WANTLIB += m pthread sqlite3 z
.else
CONFIGURE_ARGS +=	--without-sqlite3
.endif

pre-configure:
	sed -i -e "s,/usr/local/etc,${SYSCONFDIR},g" \
		${WRKSRC}/saslauthd/saslauthd.mdoc \
		${WRKSRC}/saslauthd/LDAP_SASLAUTHD

post-install:
	rm ${PREFIX}/lib/sasl2/*.a
	${INSTALL_DATA_DIR} ${PREFIX}/share/doc/cyrus-sasl
	${INSTALL_DATA_DIR} ${PREFIX}/share/examples/cyrus-sasl
	${INSTALL_DATA} ${FILESDIR}/Sendmail.conf-sql \
		${PREFIX}/share/examples/cyrus-sasl
.if ${FLAVOR:Mldap}
	${INSTALL_DATA} ${WRKSRC}/saslauthd/LDAP_SASLAUTHD \
		${PREFIX}/share/doc/cyrus-sasl
	${SUBST_DATA} ${FILESDIR}/saslauthd.conf \
		${PREFIX}/share/examples/cyrus-sasl/saslauthd.conf
.endif

.include <bsd.port.mk>
