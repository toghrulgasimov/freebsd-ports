# Created by: Steve Wills <swills@FreeBSD.org>

PORTNAME=	sidekiq
PORTVERSION=	6.2.2
CATEGORIES=	devel rubygems
MASTER_SITES=	RG
PKGNAMESUFFIX=	62

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	Simple, efficient background processing for Ruby

LICENSE=	LGPL3
LICENSE_FILE=	${WRKSRC}/LICENSE

RUN_DEPENDS=	rubygem-connection_pool>=2.2.2:net/rubygem-connection_pool \
		rubygem-rack>=2.0,3<3,3:www/rubygem-rack \
		rubygem-redis>=4.2.0:databases/rubygem-redis

USES=		cpe gem
USE_RUBY=	yes

NO_ARCH=	yes

PLIST_FILES=	bin/sidekiq \
		bin/sidekiqmon

CPE_VENDOR=	contribsys

PORTSCOUT=	limit:^6\.2\.

.include <bsd.port.mk>
