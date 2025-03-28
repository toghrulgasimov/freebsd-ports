# Created by: Po-Chuan Hsieh <sunpoet@FreeBSD.org>

PORTNAME=	myst-parser
PORTVERSION=	0.15.2
PORTREVISION=	1
CATEGORIES=	textproc python
MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	Extended commonmark compliant parser with bridges to docutils & sphinx

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE

RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}docutils>=0.15,1<0.18,1:textproc/py-docutils@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}Jinja2>=0:devel/py-Jinja2@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}markdown-it-py>=1.0.0<3.0.0:textproc/py-markdown-it-py@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}mdit-py-plugins>=0.3.0<0.4:textproc/py-mdit-py-plugins@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}yaml>=0:devel/py-yaml@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}sphinx>=3.1,1<5,1:textproc/py-sphinx@${PY_FLAVOR}

USES=		python:3.6+
USE_PYTHON=	autoplist concurrent distutils

NO_ARCH=	yes

.include <bsd.port.mk>
