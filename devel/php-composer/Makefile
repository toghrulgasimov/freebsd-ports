# Created by: Gea-Suan Lin <gslin@gslin.org>

PORTNAME=	composer
DISTVERSION=	1.10.24
CATEGORIES=	devel
MASTER_SITES=	https://getcomposer.org/download/${DISTVERSION}/
PKGNAMEPREFIX=	${PHP_PKGNAMEPREFIX}
DISTNAME=	composer
EXTRACT_SUFX=	.phar
DIST_SUBDIR=	${PORTNAME}-${PORTVERSION}

MAINTAINER=	cyberbotx@cyberbotx.com
COMMENT=	Dependency Manager for PHP

LICENSE=	MIT

DEPRECATED=	packagist.org is dropping API v1 support, please use newer 2.x version

RUN_DEPENDS=	ca_root_nss>0:security/ca_root_nss

USES=		cpe php:flavors
CPE_VENDOR=	getcomposer
USE_PHP=	ctype filter intl json mbstring openssl phar

CONFLICTS_INSTALL=	php*-composer2

NO_ARCH=	yes
NO_BUILD=	yes
NO_WRKSUBDIR=	yes

PLIST_FILES=	bin/composer \
		bin/composer.phar

do-extract:
	${MKDIR} ${WRKSRC}/
	${CP} ${_DISTDIR}/composer.phar ${WRKSRC}/

do-install:
	${INSTALL_SCRIPT} ${WRKSRC}/composer.phar ${STAGEDIR}${PREFIX}/bin/
	${LN} -s composer.phar ${STAGEDIR}${PREFIX}/bin/composer

.include <bsd.port.mk>
