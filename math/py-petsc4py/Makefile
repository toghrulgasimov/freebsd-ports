PORTNAME=	petsc4py
DISTVERSION=	3.10.0
PORTREVISION=	3
CATEGORIES=	math python
MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	yuri@FreeBSD.org
COMMENT=	PETSc for Python

LICENSE=	BSD2CLAUSE
LICENSE_FILE=	${WRKSRC}/LICENSE.rst

BROKEN=		fails to build

BUILD_DEPENDS=	${PYNUMPY}
LIB_DEPENDS=	libmpich.so:net/mpich \
		libpetsc.so:science/PETSc
RUN_DEPENDS=	${PYNUMPY}

USES=		python:3.6+
USE_PYTHON=	distutils autoplist

MAKE_ENV=	PETSC_DIR=${LOCALBASE}

.include <bsd.port.mk>
