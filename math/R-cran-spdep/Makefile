# Created by: TAKATSU Tomonari <tota@FreeBSD.org>

PORTNAME=	spdep
DISTVERSION=	1.2-1
CATEGORIES=	math
DISTNAME=	${PORTNAME}_${DISTVERSION}

MAINTAINER=	tota@FreeBSD.org
COMMENT=	Spatial dependence: weighting schemes, statistics, and models

LICENSE=	GPLv2+

CRAN_DEPENDS=	R-cran-sp>=1.0:math/R-cran-sp \
		R-cran-spData>=0.2.6.0:math/R-cran-spData \
		R-cran-sf>0:math/R-cran-sf \
		R-cran-deldir>0:math/R-cran-deldir \
		R-cran-units>0:math/R-cran-units \
		R-cran-s2>0:graphics/R-cran-s2 \
		R-cran-e1071>0:science/R-cran-e1071
BUILD_DEPENDS=	${CRAN_DEPENDS}
RUN_DEPENDS=	${CRAN_DEPENDS}

USES=	cran:auto-plist,compiles

.include <bsd.port.mk>
