PORTNAME=	aioftp
PORTVERSION=	0.20.0
CATEGORIES=	ftp python
MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	amdmi3@FreeBSD.org
COMMENT=	FTP client/server for asyncio

LICENSE=	APACHE20
LICENSE_FILE=	${WRKSRC}/license.txt

TEST_DEPENDS=	${PYTHON_PKGNAMEPREFIX}pytest>0:devel/py-pytest@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}pytest-asyncio>=0:devel/py-pytest-asyncio@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}pytest-cov>=0:devel/py-pytest-cov@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}trustme>=0:security/py-trustme@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}async_timeout>0:devel/py-async_timeout@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}siosocks>0:net/py-siosocks@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}idna>0:dns/py-idna@${PY_FLAVOR}

USES=		python:3.7+
USE_PYTHON=	autoplist distutils
NO_ARCH=	yes

do-test:
	@cd ${TEST_WRKSRC} && ${SETENV} ${TEST_ENV} ${PYTHON_CMD} -m pytest -v -rs

.include <bsd.port.mk>
