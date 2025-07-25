COMMENT=		apache HTTP server

V=			2.4.65
DISTNAME=		httpd-${V}
PKGNAME=		apache-httpd-${V}

CATEGORIES=		www net

MAINTAINER=		Giovanni Bechis <giovanni@openbsd.org>

HOMEPAGE=		https://httpd.apache.org/

# Apache 2.0
PERMIT_PACKAGE=	Yes

COMPILER=		base-clang ports-gcc
COMPILER_LANGS=		c

WANTLIB += apr-1 aprutil-1 brotlicommon brotlienc c crypto curl
WANTLIB += db expat iconv jansson lzma m nghttp2 nghttp3
WANTLIB += ngtcp2 ngtcp2_crypto_quictls pcre2-8 pthread ssl
WANTLIB += xml2 z

SITES=			${SITE_APACHE:=httpd/}

NO_TEST=		Yes

LIB_DEPENDS=		archivers/brotli \
			archivers/xz \
			devel/jansson \
			devel/pcre2 \
			net/curl \
			textproc/libxml \
			www/nghttp2

HTTPD_DIR=		/var/www
CONFDIR=		${SYSCONFDIR}/apache2
FLAVOR_COMMA=		${FLAVOR_EXT:S/-/,/g}
SUBST_VARS=		CONFDIR FLAVOR_COMMA

CONFIGURE_STYLE=	simple
DEBUG_PACKAGES=		${BUILD_PACKAGES}

CONFIGURE_ARGS=		--enable-authnz-fcgi \
			--enable-cache \
			--enable-cgi \
			--enable-disk-cache \
			--enable-socache-dc=no \
			--enable-http2 \
			--enable-layout=OpenBSD \
			--enable-lua=no \
			--enable-mods-shared=all \
			--enable-modules=all \
			--enable-mpms-shared=all \
			--enable-proxy-fdpass \
			--enable-proxy=shared \
			--enable-ssl --with-ssl=/usr \
			--enable-suexec \
			--exec-prefix=${LOCALBASE} \
			--prefix=${HTTPD_DIR} \
			--sysconfdir=${CONFDIR} \
			--with-apr-util=${LOCALBASE}/bin/apu-1-config \
			--with-apr=${LOCALBASE}/bin/apr-1-config  \
			--with-mpm=prefork \
			--with-pcre=${LOCALBASE} \
			--with-program-name=httpd2 \
			--with-suexec-bin=${TRUEPREFIX}/sbin/suexec2 \
			--with-suexec-caller=www \
			--with-suexec-logfile=${LOCALSTATEDIR}/log/suexec2_log

CONFIGURE_ENV=		CPPFLAGS="-I${LOCALBASE}/include" \
			LDFLAGS="-L${LOCALBASE}/lib" \
			AWK=awk \
			GREP=grep \
			ac_cv_func_ENGINE_init=no \
			ac_cv_path_RSYNC=no \
			ac_cv_path_SVN=no

FAKE_FLAGS=		rel_user=www rel_group=www \
			rel_datadir=${HTTPD_DIR} \
			datadir=${PREFIX}/share/examples/apache2 \
			sysconfdir=${PREFIX}/share/examples/apache2/conf

# avoid race condition from mkdir.sh during parallel install
FAKE_FLAGS +=		MKINSTALLDIRS='mkdir -p'

FLAVORS=		ldap
FLAVOR?=

.if ${FLAVOR:Mldap}
CONFIGURE_ARGS+=	--with-ldap --enable-ldap --enable-authnz-ldap
WANTLIB +=		lber-2.4 ldap-2.4 sasl2
LIB_DEPENDS +=		databases/openldap \
			apr-util->=1.6.1p0-ldap:devel/apr-util,ldap
.else
LIB_DEPENDS +=		apr-util->=1.6.1p0-!ldap:devel/apr-util
.endif

pre-configure:
	sed -i 's,%%PREFIX%%,${PREFIX},' ${WRKSRC}/config.layout
	sed -i 's,%%CONFDIR%%,${CONFDIR},' ${WRKSRC}/config.layout \
		${WRKSRC}/configure
	sed -i 's,%%PREFIX%%,${PREFIX},g' ${WRKSRC}/support/apxs.in

post-install:
	rmdir ${PREFIX}/share/examples/apache2/logs

	# avoid conflicts with httpd in base
	mv ${PREFIX}/man/man1/htpasswd.1 ${PREFIX}/man/man1/htpasswd2.1
	mv ${PREFIX}/man/man8/httpd.8 ${PREFIX}/man/man8/httpd2.8
	mv ${PREFIX}/bin/htpasswd ${PREFIX}/bin/htpasswd2

	mv ${PREFIX}/bin/apxs ${PREFIX}/sbin # other ports expect it in sbin/

	# courtesy symlinks
	for i in logresolve dbmmanage htdigest; do ln -s $${i} ${PREFIX}/bin/$${i}2; done
	for i in apachectl apxs rotatelogs suexec; do ln -s $${i} ${PREFIX}/sbin/$${i}2; done

.if ${FLAVOR:Mldap}
	${INSTALL_DATA_DIR} ${PREFIX}/share/doc/ap2-mod_auth_ldap
.for i in mod_ldap.html mod_authnz_ldap.html.en \
	mod_authnz_ldap.html mod_ldap.html.en
	${INSTALL_DATA} ${WRKSRC}/docs/manual/mod/${i} \
		${PREFIX}/share/doc/ap2-mod_auth_ldap/
.endfor
.endif

.include <bsd.port.mk>
