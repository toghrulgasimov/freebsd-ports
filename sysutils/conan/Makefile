PORTNAME=	conan
DISTVERSION=	1.44.0
CATEGORIES=	sysutils python
MASTER_SITES=	CHEESESHOP

MAINTAINER=	yuri@FreeBSD.org
COMMENT=	C/C++ package manager

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE.md

PY_DEPENDS=	\
		${PYTHON_PKGNAMEPREFIX}bottle>=0.12.8:www/py-bottle@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}colorama>=0.3.3,<0.5.0:devel/py-colorama@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}dateutil>=2.7.0,<3:devel/py-dateutil@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}deprecation>=2.0:devel/py-deprecation@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}distro>=1.0.2:sysutils/py-distro@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}fasteners>=0.14.1:devel/py-fasteners@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}future>=0.16.0,<0.19.0:devel/py-future@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}Jinja2>=2.9:devel/py-Jinja2@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}node-semver>=0.6.1:devel/py-node-semver@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}patch-ng>=1.17.4,<1.18:devel/py-patch-ng@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}pluginbase>=0.5:devel/py-pluginbase@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}pygments>=2.0,<3.0:textproc/py-pygments@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}pyjwt1>=1.4.0,<2.0.0:www/py-pyjwt1@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}requests>=2.25,<3.0.0:www/py-requests@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}six>=1.10.0,<=1.16.0:devel/py-six@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}sqlite3>0:databases/py-sqlite3@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}urllib3>=1.26.6,1<1.27,1:net/py-urllib3@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}tqdm>=4.28.1,<5:misc/py-tqdm@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}yaml>=3.11,<6.0:devel/py-yaml@${PY_FLAVOR}
BUILD_DEPENDS=	${PY_DEPENDS}
RUN_DEPENDS=	${PY_DEPENDS}

USES=		python
USE_PYTHON=	distutils noflavors autoplist

NO_ARCH=	yes

.include <bsd.port.mk>
