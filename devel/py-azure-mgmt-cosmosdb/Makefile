PORTNAME=	azure-mgmt-cosmosdb
PORTVERSION=	7.0.0b2
CATEGORIES=	devel python
MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	dbaio@FreeBSD.org
COMMENT=	Microsoft Azure Cosmos DB Management Client Library for Python

LICENSE=	MIT

RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}msrest>=0.6.21:net-mgmt/py-msrest@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}azure-common>=1.1:www/py-azure-common@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}azure-mgmt-core>=1.2.0<2.0.0:devel/py-azure-mgmt-core@${PY_FLAVOR}

USES=		azurepy python:3.6+ zip
USE_PYTHON=	autoplist concurrent distutils

NO_ARCH=	yes

.include <bsd.port.mk>
