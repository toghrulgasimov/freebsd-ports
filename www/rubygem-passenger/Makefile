# Created by: Jacob Atzen <jatzen@gmail.com>

PORTNAME=	passenger
PORTVERSION=	6.0.12
PORTREVISION=	2
CATEGORIES=	www rubygems
MASTER_SITES=	RG
PATCH_SITES=	https://github.com/phusion/passenger/commit/
PATCHFILES=	4c8d0a1316000db93eb4484480b2e14188560e14.patch:-p1 \
		9640816af708867d0994bd2eddb80ac24399f855.patch:-p1

MAINTAINER=	osa@FreeBSD.org
COMMENT=	Modules for running Ruby on Rails and Rack applications

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE

BUILD_DEPENDS=	rake:devel/rubygem-rake

CPE_VENDOR=	phusion
CPE_PRODUCT=	passenger

FLAVORS=	apache nginx
FLAVOR?=	${FLAVORS:[1]}

apache_PKGNAMESUFFIX=	-apache
nginx_PKGNAMESUFFIX=	-nginx

apache_CONFLICTS_INSTALL=	${PKGNAMEPREFIX}${PORTNAME}-nginx
nginx_CONFLICTS_INSTALL=	${PKGNAMEPREFIX}${PORTNAME}-apache

OPTIONS_DEFINE=	DEBUG SYMLINK
OPTIONS_DEFAULT=SYMLINK
OPTIONS_EXCLUDE=DOCS
SYMLINK_DESC=	Create passenger symlink

.if ${FLAVOR} == apache
USES+=		apache:2.2+
.endif

USE_RUBY=	yes
RAKE_BIN=	${LOCALBASE}/bin/rake
USES+=		compiler:c++11-lang cpe gem libtool python:env shebangfix ssl
SHEBANG_FILES=	src/cxx_supportlib/vendor-copy/libuv/gyp_uv.py

LIB_DEPENDS+=	libuv.so:devel/libuv \
		libcurl.so:ftp/curl \
		libapr-1.so:devel/apr1

BUILD_DEPENDS+=	rubygem-rack>=0:www/rubygem-rack
RUN_DEPENDS:=	${BUILD_DEPENDS} \
		rubygem-etc>=0:devel/rubygem-etc

SUB_LIST+=	GEM_LIB_DIR=${GEM_LIB_DIR} RUBY=${RUBY}
SUB_FILES=	pkg-message-${FLAVOR}

PLIST_FILES=	bin/passenger \
		bin/passenger-config \
		bin/passenger-memory-stats \
		bin/passenger-status

SYMLINK_PLIST_FILES=	${GEMS_DIR}/${PORTNAME}
SYMLINK_SUB_LIST=	PASSENGER_INSTALL_DIR="${PREFIX}/${GEMS_DIR}/${PORTNAME}"
SYMLINK_SUB_LIST_OFF=	PASSENGER_INSTALL_DIR="${PREFIX}/${GEM_LIB_DIR}"

pre-patch:
	@${REINPLACE_CMD} \
		's!-Wall!!g; \
		s!gcc!${CC}!g; \
		s!g++!${CXX}!g; \
		s!#{PlatformInfo.debugging_cflags}!${CFLAGS}!g; \
		s!-O2!!g; \
		s! -feliminate-unused-debug-symbols -feliminate-unused-debug-types!!g; \
		170s!true!false!' \
		${WRKSRC}/build/basics.rb
	@${REINPLACE_CMD} '1s:python:python2:' \
		${WRKSRC}/src/cxx_supportlib/vendor-copy/libuv/gyp_uv.py

pre-patch-DEBUG-off:
	@${REINPLACE_CMD} \
		's!-DPASSENGER_DEBUG!-DNDEBUG!g' \
		${WRKSRC}/build/basics.rb

post-build:
.if ${FLAVOR} == apache
	(CC=${CC} CXX=${CXX} ${WRKSRC}/bin/passenger-install-apache2-module --auto)
.endif

.if ${FLAVOR} == nginx
	(cd ${WRKSRC} && CC=${CC} CXX=${CXX} ${RAKE_BIN} nginx)
.endif
	${FIND} ${WRKSRC} -name '*.o' -o -name '*.bak' -o -name '*.orig' | ${XARGS} ${RM}

post-install:
	( cd ${WRKSRC} && \
	${COPYTREE_SHARE} buildout ${STAGEDIR}${PREFIX}/${GEMS_DIR}/${PORTNAME}-${PORTVERSION} )
	${CHMOD} +x ${STAGEDIR}${PREFIX}/${GEMS_DIR}/${PORTNAME}-${PORTVERSION}/buildout/support-binaries/*
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/${GEM_LIB_DIR}/buildout/ruby/*/passenger_native_support.so
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/${GEM_LIB_DIR}/buildout/support-binaries/PassengerAgent
	${FIND} ${STAGEDIR}${PREFIX}/${GEM_LIB_DIR} -type d -empty -delete
.if ${FLAVOR} == apache
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/${GEM_LIB_DIR}/buildout/apache2/mod_passenger.so
	${MKDIR} ${STAGEDIR}${PREFIX}/${APACHEMODDIR}
	${LN} -sf ../../${GEM_LIB_DIR}/buildout/apache2/mod_passenger.so ${STAGEDIR}${PREFIX}/${APACHEMODDIR}/mod_passenger.so
	@${ECHO} "${APACHEMODDIR}/mod_passenger.so" >> ${TMPPLIST}
.endif
	@${RM} ${STAGEDIR}${PREFIX}/bin/passenger-install-apache2-module \
		${STAGEDIR}${PREFIX}/bin/passenger-install-nginx-module
	@${RM} ${STAGEDIR}${PREFIX}/${GEM_LIB_DIR}/bin/passenger-install-apache2-module \
		${STAGEDIR}${PREFIX}/${GEM_LIB_DIR}/bin/passenger-install-nginx-module

post-install-SYMLINK-on:
	${LN} -s ${GEM_NAME} ${STAGEDIR}${PREFIX}/${GEMS_DIR}/${PORTNAME}

.include <bsd.port.mk>
