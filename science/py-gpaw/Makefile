PORTNAME=	gpaw
DISTVERSION=	21.6.0
PORTREVISION=	1
CATEGORIES=	science python
MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	yuri@FreeBSD.org
COMMENT=	DFT and beyond within the projector-augmented wave method in chemistry

LICENSE=	GPLv3+
LICENSE_FILE=	${WRKSRC}/LICENSE

BUILD_DEPENDS=	${PYNUMPY}
LIB_DEPENDS=	libblas.so:math/blas \
		libmpich.so:net/mpich \
		libopenblas.so:math/openblas \
		libxc.so:science/libxc
RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}ase>0:science/py-ase@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}matplotlib>0:math/py-matplotlib@${PY_FLAVOR} \
		${PYNUMPY} \
		${PYTHON_PKGNAMEPREFIX}scipy>=0:science/py-scipy@${PY_FLAVOR} \
		gpaw-setups>0:science/gpaw-setups

USES=		gettext-runtime localbase python:3.7+ shebangfix
USE_PYTHON=	distutils concurrent autoplist
SHEBANG_FILES=	tools/*

LDFLAGS=	-lmpi # otherwise: ImportError: /usr/local/lib/python3.8/site-packages/_gpaw.cpython-38.so: Undefined symbol "MPI_Comm_rank"

post-patch:
	@${REINPLACE_CMD} "s|'/usr/local/|'${LOCALBASE}/|" ${WRKSRC}/gpaw/__init__.py

post-install:
	@${STRIP_CMD} ${STAGEDIR}${PYTHONPREFIX_SITELIBDIR}/_gpaw*.so

.include <bsd.port.mk>
