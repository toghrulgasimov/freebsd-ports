# Created by: Po-Chuan Hsieh <sunpoet@FreeBSD.org>

PORTNAME=	publicsuffixlist
PORTVERSION=	0.7.10
PORTREVISION=	2
CATEGORIES=	dns python
MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	Publicsuffixlist implementation

LICENSE=	MPL20
LICENSE_FILE=	${WRKSRC}/LICENSE

PATCH_DEPENDS=	public_suffix_list>=0:dns/public_suffix_list

USES=		python:3.6+
USE_PYTHON=	autoplist concurrent distutils

NO_ARCH=	yes

post-patch:
	@${CP} ${LOCALBASE}/share/public_suffix_list/public_suffix_list.dat ${WRKSRC}/publicsuffixlist/public_suffix_list.dat
	@${CP} ${LOCALBASE}/share/public_suffix_list/test_psl.txt ${WRKSRC}/publicsuffixlist/test_psl.txt

.include <bsd.port.mk>
