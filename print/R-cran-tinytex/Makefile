PORTNAME=	tinytex
DISTVERSION=	0.36
CATEGORIES=	print
DISTNAME=	${PORTNAME}_${DISTVERSION}

MAINTAINER=	tota@FreeBSD.org
COMMENT=	Helper functions to maintain LaTeX distribution

LICENSE=	MIT

CRAN_DEPENDS=	R-cran-xfun>=0.29:misc/R-cran-xfun
BUILD_DEPENDS=	${CRAN_DEPENDS}
RUN_DEPENDS=	${CRAN_DEPENDS}

USES=		cran:auto-plist

.include <bsd.port.mk>
