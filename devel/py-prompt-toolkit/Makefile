# Created by: Steven Kreuzer <skreuzer@FreeBSD.org>

PORTNAME=	prompt-toolkit
PORTVERSION=	3.0.23
CATEGORIES=	devel python
MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}
DISTNAME=	prompt_toolkit-${PORTVERSION}

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	Library for building powerful interactive command lines in Python

LICENSE=	BSD3CLAUSE
LICENSE_FILE=	${WRKSRC}/LICENSE

RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}wcwidth>=0:devel/py-wcwidth@${PY_FLAVOR}

USES=		python:3.6+
USE_PYTHON=	autoplist concurrent distutils

NO_ARCH=	yes

.include <bsd.port.mk>
