BROKEN-sparc64=	doesn't detect Ruby library in configure

UNIT_MODNAME=	ruby${MODRUBY_REV}
UNIT_SHORTNAME=	ruby
REVISION=	0

MODULES+=	lang/ruby

# XXX ruby port provide librubyXX.so which is picked up in preference to
# the versioned library. Keep the "Extra" WANTLIB.
WANTLIB=	${MODRUBY_WANTLIB}
CONFIGURE_ENV+=	RUBY=${RUBY}
LIB_DEPENDS=	${MODRUBY_LIB_DEPENDS}
RUN_DEPENDS=	${MODRUBY_RUN_DEPENDS}
SUBST_VARS=	MODRUBY_REV

post-configure:
	cd ${WRKSRC} && ./configure ruby --ruby=${MODRUBY_FLAVOR} \
	    --module=ruby${MODRUBY_REV}
	/usr/bin/sed -i -e 's/-Werror //' ${WRKSRC}/build/Makefile

# needed for ruby 3 on llvm
CFLAGS-base_clang+=	-fdeclspec

.include <bsd.port.mk>
