# Created by: Po-Chuan Hsieh <sunpoet@FreeBSD.org>

PORTNAME=	ddtrace
PORTVERSION=	0.56.1
CATEGORIES=	devel python
MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	Datadog APM client library

LICENSE=	APACHE20 BSD3CLAUSE
LICENSE_COMB=	dual
LICENSE_FILE_APACHE20=	${WRKSRC}/LICENSE.Apache
LICENSE_FILE_BSD3CLAUSE=${WRKSRC}/LICENSE.BSD3

BUILD_DEPENDS=	${PYTHON_PKGNAMEPREFIX}setuptools_scm>=4:devel/py-setuptools_scm@${PY_FLAVOR}
RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}protobuf>=3,1:devel/py-protobuf@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}tenacity>=5:devel/py-tenacity@${PY_FLAVOR}

USES=		compiler:c11 python:3.6+
USE_PYTHON=	autoplist concurrent cython distutils

OPTIONS_DEFINE=	OPENTRACING
OPTIONS_DEFAULT=OPENTRACING
OPENTRACING_DESC=	OpenTracing support

OPENTRACING_RUN_DEPENDS=${PYTHON_PKGNAMEPREFIX}opentracing>=2.0.0:devel/py-opentracing@${PY_FLAVOR}

.include <bsd.port.pre.mk>

.if ${PYTHON_REL} < 30700
RUN_DEPENDS+=	${PYTHON_PKGNAMEPREFIX}pep562>=0:devel/py-pep562@${PY_FLAVOR}
.endif

post-patch:
	@${RM} ${WRKSRC}/ddtrace/profiling/collector/stack.c

post-install:
	${FIND} ${STAGEDIR}${PYTHON_SITELIBDIR} -name '*.so' -exec ${STRIP_CMD} {} +

.include <bsd.port.post.mk>
