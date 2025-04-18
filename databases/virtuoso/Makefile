# Created by: Max Khon <fjoe@FreeBSD.org>

PORTNAME=	virtuoso
PORTVERSION=	7.2.5
PORTREVISION=	1
CATEGORIES=	databases
MASTER_SITES=	SF
DISTNAME=	${PORTNAME}-opensource-${PORTVERSION}

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Universal SQL/Application Server

LICENSE=	GPLv2
LICENSE_FILE=	${WRKSRC}/COPYING

BROKEN_aarch64=		Fails to link: missing sbrk
BROKEN_mips64=		Does not compile: error: DV_INT_TAG_WORD undeclared
BROKEN_powerpc64=	Does not compile: error: DV_INT_TAG_WORD undeclared
BROKEN_sparc64=		Does not compile: error: DV_INT_TAG_WORD undeclared
NOT_FOR_ARCHS=		armv6 armv7 i386 mips powerpc powerpcspe
NOT_FOR_ARCHS_REASON=	can only be built on 64bit platforms

BUILD_DEPENDS=	gawk:lang/gawk\
		htmldoc:textproc/htmldoc\
		flex>2.5.4:textproc/flex\
		gperf>=3.0.3:devel/gperf
LIB_DEPENDS=	libxml2.so:textproc/libxml2

USES=		gmake libtool readline uidfix ssl

GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--with-readline\
		--without-internal-zlib\
		--without-jdk2\
		--without-jdk3\
		--without-jdk4\
		--disable-hslookup\
		--disable-wbxml2\
		--with-layout=freebsd\
		--datadir="${PREFIX}"\
		--localstatedir="${PREFIX}"
CONFIGURE_ENV=	ac_cv_header_sys_timeb_h=no
CPPFLAGS+=	-std=gnu89
LDFLAGS+=	-lexecinfo
MAKE_ENV=	PATH=${LOCALBASE}/bin:${PATH}\
		ISQL=isql-vt
USE_RC_SUBR=	virtuoso
USERS=		virtuoso
GROUPS=		virtuoso
SUB_FILES=	pkg-message

CHECK_PORT=	nc -z localhost $$\1 2>\&1

OPTIONS_DEFINE=		IMAGEMAGICK KERBEROS LDAP IODBC

post-patch:
	${REINPLACE_CMD} -e 's,-lruby,-lruby${RUBY_SUFFIX},g'\
			${WRKSRC}/configure
	${FIND} ${WRKSRC} -name '*.sh' | ${XARGS} ${GREP} -l 'netstat -an.*grep LISTEN' |\
	    ${XARGS} ${REINPLACE_CMD}\
		-e 's,expr \$$,expr -- $$,'\
		-e 's,netstat -an.*grep.*$$\([a-zA-Z0-9]*\).*grep LISTEN,${CHECK_PORT},'

check:
	${SETENV} -u HOST ${MAKE_ENV} ${MAKE} -C ${WRKSRC} check

.include <bsd.port.options.mk>

.if ${SSL_DEFAULT} == base
BROKEN_FreeBSD_12=	OpenSSL version 1.1.0 or greater is currently not supported
BROKEN_FreeBSD_13=	OpenSSL version 1.1.0 or greater is currently not supported
BROKEN_FreeBSD_14=	OpenSSL version 1.1.0 or greater is currently not supported
.endif

.if ${PORT_OPTIONS:MIMAGEMAGICK}
CONFIGURE_ARGS+=--enable-imagemagick=${LOCALBASE}
USES+=		magick:6
PLIST_SUB+=	WITH_IMAGEMAGICK=""
.else
CONFIGURE_ARGS+=--disable-imagemagick
PLIST_SUB+=	WITH_IMAGEMAGICK="@comment "
.endif

.if ${PORT_OPTIONS:MIODBC}
CONFIGURE_ARGS+=--with-iodbc=${LOCALBASE}
LIB_DEPENDS+=	libiodbc.so:databases/libiodbc
CPPFLAGS+=	-I${LOCALBASE}/include/libiodbc
PLIST_SUB+=	WITH_IODBC=""
.else
CPPFLAGS+=	-I../../libsrc/odbcsdk/include
PLIST_SUB+=	WITH_IODBC="@comment "
.endif

.if ${PORT_OPTIONS:MKERBEROS}
CONFIGURE_ARGS+=--enable-krb=${LOCALBASE}
LIB_DEPENDS+=	libkrb5.so:security/krb5
.else
CONFIGURE_ARGS+=--disable-krb
.endif

.if ${PORT_OPTIONS:MLDAP}
CONFIGURE_ARGS+=--enable-openldap=${LOCALBASE}
USE_OPENLDAP=	yes
.else
CONFIGURE_ARGS+=--disable-openldap
.endif

post-install:
	${FIND} ${STAGEDIR} -name "*.ini" -exec ${MV} {} {}.sample \; -print
	${RMDIR} ${STAGEDIR}${PREFIX}/virtuoso/doc/html

.include <bsd.port.mk>
