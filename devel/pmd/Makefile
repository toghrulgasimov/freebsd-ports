# Created by: Alex Varju <freebsd-ports@varju.ca>

PORTNAME=	pmd
PORTVERSION=	6.41.0
CATEGORIES=	devel java
MASTER_SITES=	SF
DISTNAME=	${PORTNAME}-bin-${PORTVERSION}

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Static analysis tool for Java source code

LICENSE=	APACHE20 BSD4CLAUSE
LICENSE_COMB=	dual

USES=		cpe zip

CPE_VENDOR=	pmd_project
USE_JAVA=	yes
NO_BUILD=	yes
DATADIR=	${JAVASHAREDIR}/${PORTNAME}
PLIST_SUB+=	PORTVERSION=${PORTVERSION}

post-patch:
	@${REINPLACE_CMD} -e 's|#!/bin/bash|#!/bin/sh|' -e 's|function||' \
		-e 's|LIB_DIR=$$(pwd -P)|LIB_DIR=${DATADIR}|' ${WRKSRC}/bin/run.sh

do-install:
	${INSTALL_SCRIPT} ${WRKSRC}/bin/run.sh ${STAGEDIR}${PREFIX}/bin/pmd
	@${MKDIR} ${STAGEDIR}${DATADIR}
	${INSTALL_DATA} ${WRKSRC}/lib/* ${STAGEDIR}${DATADIR}

.include <bsd.port.mk>
