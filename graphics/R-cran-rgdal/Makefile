# Created by: TAKATSU Tomonari <tota@FreeBSD.org>

PORTNAME=	rgdal
DISTVERSION=	1.5-28
CATEGORIES=	graphics
DISTNAME=	${PORTNAME}_${DISTVERSION}

MAINTAINER=	tota@FreeBSD.org
COMMENT=	Bindings for the Geospatial Data Abstraction Library

LICENSE=	GPLv2+

LIB_DEPENDS=	libgdal.so:graphics/gdal \
		libproj.so:graphics/proj
CRAN_DEPENDS=	R-cran-sp>=1.1.0:math/R-cran-sp
BUILD_DEPENDS=	${CRAN_DEPENDS}
RUN_DEPENDS=	${CRAN_DEPENDS}

USES=		compiler:c++11-lang cran:auto-plist,compiles pkgconfig

.include <bsd.port.mk>
