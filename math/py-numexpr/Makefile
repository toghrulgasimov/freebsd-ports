# Created by: Ju Pengfei <ju.pengfei@gmail.com>

PORTNAME=	numexpr
PORTVERSION=	2.8.0
DISTVERSIONPREFIX=	v
CATEGORIES=	math python
#MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	Fast numerical array expression evaluator for Python and NumPy

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE.txt

BUILD_DEPENDS=	${RUN_DEPENDS}
RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}numpy>=1.7,1:math/py-numpy@${PY_FLAVOR}

USES=		dos2unix python:3.7+
USE_PYTHON=	autoplist concurrent distutils

GH_ACCOUNT=	pydata
USE_GITHUB=	yes

post-install:
	${FIND} ${STAGEDIR}${PYTHON_SITELIBDIR} -name '*.so' -exec ${STRIP_CMD} {} +

.include <bsd.port.mk>
