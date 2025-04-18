# Created by: Po-Chuan Hsieh <sunpoet@FreeBSD.org>

PORTNAME=	ipykernel
PORTVERSION=	6.6.0
CATEGORIES=	devel python
MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	IPython Kernel for Jupyter

LICENSE=	BSD3CLAUSE
LICENSE_FILE=	${WRKSRC}/COPYING.md

RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}debugpy>=1.0.0<2.0:devel/py-debugpy@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}ipython>=7.23.1:devel/ipython@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}jupyter-client>=0<8.0:devel/py-jupyter-client@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}matplotlib-inline>=0.1.0<0.2.0:math/py-matplotlib-inline@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}tornado>=4.2<7.0:www/py-tornado@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}traitlets>=5.1.0<6.0:devel/py-traitlets@${PY_FLAVOR}

USES=		python:3.7+
USE_PYTHON=	autoplist concurrent distutils

NO_ARCH=	yes

.include <bsd.port.pre.mk>

.if ${PYTHON_REL} < 30800
RUN_DEPENDS+=	${PYTHON_PKGNAMEPREFIX}argcomplete>=0<1.12.4:devel/py-argcomplete@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}importlib-metadata>=0<5:devel/py-importlib-metadata@${PY_FLAVOR}
.endif

.include <bsd.port.post.mk>
