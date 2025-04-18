# Created by: Joseph Koshy <jkoshy@FreeBSD.org>

PORTNAME=	fonttools
PORTVERSION=	4.28.2
CATEGORIES=	print python
MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	Open source library for manipulating fonts, written in Python

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE

TEST_DEPENDS=	${PYTHON_PKGNAMEPREFIX}ufolib2>=0:print/py-ufolib2@${PY_FLAVOR}

USES=		python:3.7+ zip
USE_PYTHON=	autoplist concurrent distutils

MAKE_ENV=	FONTTOOLS_MANPATH="man"
NO_ARCH=	yes

OPTIONS_DEFINE=	GRAPHITE INTERPOLATABLE LXML PLOT SYMFONT UFO UNICODE WOFF
OPTIONS_DEFAULT=LXML UFO UNICODE

GRAPHITE_DESC=	Process graphite type tables in ttLib/tables
INTERPOLATABLE_DESC=	Interpolatability support
LXML_DESC=	Read/write XML files via lxml (faster/safer than built-in ElementTree)
PLOT_DESC=	Visualize DesignSpaceDocument and resulting VariationModel
SYMFONT_DESC=	Symbolic font statistics analysis
UFO_DESC=	Read/write UFO fonts
UNICODE_DESC=	Use latest Unicode Character Database
WOFF_DESC=	Compress/uncompress WOFF webfonts

GRAPHITE_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}lz4>=1.7.4.2:archivers/py-lz4@${PY_FLAVOR}
INTERPOLATABLE_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}scipy>=0:science/py-scipy@${PY_FLAVOR}
LXML_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}lxml>=4.0<5:devel/py-lxml@${PY_FLAVOR}
PLOT_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}matplotlib>=0:math/py-matplotlib@${PY_FLAVOR}
SYMFONT_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}sympy>=0:math/py-sympy@${PY_FLAVOR}
UFO_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}fs2>=2.2.0<3:devel/py-fs2@${PY_FLAVOR}
UNICODE_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}unicodedata2>=13.0.0.post2:devel/py-unicodedata2@${PY_FLAVOR}
WOFF_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}brotli>=1.0.1:archivers/py-brotli@${PY_FLAVOR} \
			${PYTHON_PKGNAMEPREFIX}zopfli>=0.1.4:archivers/py-zopfli@${PY_FLAVOR}

.include <bsd.port.mk>
