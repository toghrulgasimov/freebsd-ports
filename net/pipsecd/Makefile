# Created by: Patrick Bihan-Faou <patrick@mindstep.com>

PORTNAME=	pipsecd
PORTVERSION=	19991014
PORTREVISION=	6
CATEGORIES=	net security
MASTER_SITES=	http://www.komquats.com/distfiles/ \
		LOCAL/cy
DISTNAME=	pipsec-19991014

MAINTAINER=	cy@FreeBSD.org
COMMENT=	Simple IPSEC tunnel tool from Pierre Beyssac

DEPRECATED=	Abandonware, current release is from 1999 and uses insecure encryption algorithms
EXPIRATION_DATE=2022-01-15

USES+=		ssl

USE_RC_SUBR=	pipsecd

ALL_TARGET=	pipsecd

OPTIONS_DEFINE=	DOCS

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/pipsecd ${STAGEDIR}${PREFIX}/sbin
	${MKDIR} ${STAGEDIR}${PREFIX}/etc/ipsec
	${INSTALL_DATA} ${WRKSRC}/pipsecd.conf.sample ${STAGEDIR}${PREFIX}/etc/ipsec
	${MKDIR} ${STAGEDIR}${PREFIX}/share/doc/pipsecd
	${INSTALL_DATA} ${WRKSRC}/README ${STAGEDIR}${PREFIX}/share/doc/pipsecd
	${INSTALL_DATA} ${WRKSRC}/COPYRIGHT ${STAGEDIR}${PREFIX}/share/doc/pipsecd
	${INSTALL_DATA} ${WRKSRC}/README.port ${STAGEDIR}${PREFIX}/share/doc/pipsecd

.include <bsd.port.mk>
