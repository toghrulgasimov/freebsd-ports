PORTNAME=	pytest-relaxed
PORTVERSION=	1.1.5
PORTREVISION=	1
CATEGORIES=	devel python
MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	koobs@FreeBSD.org
COMMENT=	Relaxed test discovery/organization for pytest

LICENSE=	BSD2CLAUSE
LICENSE_FILE=	${WRKSRC}/LICENSE

DEPRECATED=	Depends on expired devel/py-decorator4
EXPIRATION_DATE=2022-03-31

RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}pytest>=3<5:devel/py-pytest@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}six>=1<2:devel/py-six@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}decorator4>=4<5:devel/py-decorator4@${PY_FLAVOR}

USES=		python:3.6+
USE_PYTHON=	autoplist distutils

NO_ARCH=	yes

do-test:
	 @cd ${WRKSRC} && ${PYTHON_CMD} -m pytest -v -rs

.include <bsd.port.mk>
