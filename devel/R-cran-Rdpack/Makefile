PORTNAME=	Rdpack
DISTVERSION=	2.1.3
CATEGORIES=	devel
DISTNAME=	${PORTNAME}_${DISTVERSION}

MAINTAINER=	tota@FreeBSD.org
COMMENT=	Update and Manipulate Rd Documentation Objects

LICENSE=	GPLv2+

CRAN_DEPENDS=	R-cran-rbibutils>=1.3:textproc/R-cran-rbibutils
BUILD_DEPENDS=	${CRAN_DEPENDS}
RUN_DEPENDS=	${CRAN_DEPENDS}

USES=		cran:auto-plist

.include <bsd.port.mk>
