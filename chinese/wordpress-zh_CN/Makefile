# Created by: Joe Horn <joehorn@gmail.com>

PORTNAME=	wordpress
DISTVERSION=	5.8.2
DISTVERSIONSUFFIX=	-zh_CN
CATEGORIES=	chinese www
MASTER_SITES=	https://cn.wordpress.org/
PKGNAMESUFFIX=	-zh_CN

MAINTAINER=	joneum@FreeBSD.org
COMMENT=	State-of-the-art semantic personal publishing platform

LICENSE=	GPLv2+
LICENSE_FILE=	${WRKSRC}/license.txt

RUN_DEPENDS=	${LOCALBASE}/lib/php/${PHP_EXT_DIR}/imagick.so:graphics/pecl-imagick@${PHP_FLAVOR}

USES=		cpe php:web
.if ${DISTVERSION:N*.*.*}
CPE_VERSION=	${DISTVERSION}.0
.endif
USE_PHP=	curl exif fileinfo ftp gd hash json mysqli pcre tokenizer xml zip zlib
WWWDIR=		${PREFIX}/www/${PORTNAME}${PKGNAMESUFFIX}
NO_ARCH=	yes
NO_BUILD=	yes
SUB_FILES=	pkg-message
WRKSRC=		${WRKDIR}/${PORTNAME}
PLIST=		${WRKDIR}/pkg-plist
PORTDOCS=	readme.html
OPTIONS_DEFINE=	DOCS

pre-everything::
	@${ECHO_CMD} "If you want to upgrade, you must read upgrade document."
	@${ECHO_CMD} ""
.  if !(defined(PACKAGE_BUILDING) || defined(BATCH))
	@sleep 1
.  endif

pre-install:
	${ECHO_CMD} '@owner www' > ${PLIST}
	${ECHO_CMD} '@group www' >> ${PLIST}
	cd ${WRKSRC}/ && ${FIND} -s * -type f | ${SED} -e 's|^|%%WWWDIR%%/|' >> ${PLIST}
	${ECHO_CMD} '@owner' >> ${PLIST}
	${ECHO_CMD} '@group' >> ${PLIST}
	if [ ! -f ${WRKSRC}/wp-config-sample.php ]; then ${CP} \
		${WRKSRC}/wp-config.php.sample ${WRKSRC}/wp-config.php; fi

do-install:
	${INSTALL} -d -m 755 ${STAGEDIR}${WWWDIR}/
	${CP} -R ${WRKSRC}/ ${STAGEDIR}${WWWDIR}/
	${FIND} ${STAGEDIR}${WWWDIR}/ -type d -exec ${CHMOD} g+w {} \;

do-install-DOCS-on:
	${MKDIR} ${STAGEDIR}${DOCSDIR}/
	cd ${WRKSRC}/ && ${INSTALL_DATA} ${PORTDOCS} ${STAGEDIR}${DOCSDIR}/

.include <bsd.port.mk>
