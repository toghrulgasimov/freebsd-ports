# Created by: Craig Leres <leres@FreeBSD.org>

PORTNAME=	arduino-sevseg
PORTVERSION=	3.7.0
DISTVERSIONPREFIX=	v
CATEGORIES=	devel

MAINTAINER=	leres@FreeBSD.org
COMMENT=	Arduino seven segment display library

LICENSE=	MIT

USE_GITHUB=	yes
GH_ACCOUNT=	DeanIsMe
GH_PROJECT=	SevSeg

NO_BUILD=	yes

FILES=		SevSeg.cpp SevSeg.h keywords.txt

PLIST_FILES=	${FILES:S,^,arduino/libraries/SevSeg/,}
PORTEXAMPLES=	*

OPTIONS_DEFINE=	EXAMPLES

do-install:
	${MKDIR} ${STAGEDIR}${PREFIX}/arduino/libraries/SevSeg
	(cd ${WRKSRC} && ${INSTALL_DATA} ${FILES} \
		${STAGEDIR}${PREFIX}/arduino/libraries/SevSeg)
	${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	cd ${WRKSRC}/examples && ${COPYTREE_SHARE} . ${STAGEDIR}${EXAMPLESDIR}

.include <bsd.port.mk>
