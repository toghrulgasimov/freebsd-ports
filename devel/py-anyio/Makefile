# Created by: Po-Chuan Hsieh <sunpoet@FreeBSD.org>

PORTNAME=	anyio
PORTVERSION=	3.4.0
CATEGORIES=	devel python
MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	High level compatibility layer for multiple asynchronous event loop implementations

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE

BUILD_DEPENDS=	${PYTHON_PKGNAMEPREFIX}setuptools_scm>=3.4:devel/py-setuptools_scm@${PY_FLAVOR}
RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}idna>=2.8:dns/py-idna@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}sniffio>=1.1:devel/py-sniffio@${PY_FLAVOR}

USES=		python:3.7+
USE_PYTHON=	autoplist concurrent distutils

NO_ARCH=	yes

OPTIONS_DEFINE=	TRIO
TRIO_DESC=	Use trio as backend

TRIO_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}trio>=0.16:net/py-trio@${PY_FLAVOR}

.include <bsd.port.pre.mk>

.if ${PYTHON_REL} < 30800
RUN_DEPENDS+=	${PYTHON_PKGNAMEPREFIX}typing-extensions>=0:devel/py-typing-extensions@${PY_FLAVOR}
.endif

.include <bsd.port.post.mk>
