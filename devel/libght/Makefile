# Created by: lbartoletti <lbartoletti@FreeBSD.org>

PORTNAME=	libght
PORTVERSION=	0.1.0
PORTREVISION=	3
DISTVERSIONPREFIX=	v
CATEGORIES=	devel geography

MAINTAINER=	lbartoletti@FreeBSD.org
COMMENT=	GeoHashTree library for storing and accessing multi-dimensional point clouds

LICENSE=	BSD3CLAUSE
LICENSE_FILE=	${WRKSRC}/COPYRIGHT

LIB_DEPENDS=	libproj.so:graphics/proj \
		liblas.so:devel/liblas \
		libcunit.so:devel/cunit

USES=		cmake gnome
USE_GNOME=	libxml2
USE_LDCONFIG=	yes

USE_GITHUB=	yes
GH_ACCOUNT=	pramsey

.include <bsd.port.mk>
