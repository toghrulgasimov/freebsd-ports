# Created by: nbm

PORTNAME=	pycrypto
PORTVERSION=	2.6.1
PORTREVISION=	3
CATEGORIES=	security python
MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	koobs@FreeBSD.org
COMMENT=	Python Cryptography Toolkit

LICENSE=	PD
LICENSE_FILE=	${WRKSRC}/COPYRIGHT

CONFLICTS_INSTALL=	${PYTHON_PKGNAMEPREFIX}pycryptodome

USES=		cpe python:3.6-3.10
USE_PYTHON=	distutils autoplist

CPE_VENDOR=	dlitz

GNU_CONFIGURE=	yes

OPTIONS_DEFINE=		GMP
OPTIONS_DEFAULT=	GMP

GMP_DESC=		Use GMP for faster DSA/RSA operations
GMP_CONFIGURE_WITH=	gmp
GMP_CPPFLAGS=		-I${LOCALBASE}/include
GMP_LDFLAGS=		-L${LOCALBASE}/lib
GMP_LIB_DEPENDS=	libgmp.so:math/gmp

pre-patch:
	@${REINPLACE_CMD} -e "s|%%LOCALBASE%%|${LOCALBASE}|" ${WRKSRC}/setup.py

post-install:
	@${STRIP_CMD} ${STAGEDIR}${PYTHONPREFIX_SITELIBDIR}/Crypto/*/*.so

regression-test: build
	@cd ${WRKSRC} && ${PYTHON_CMD} ${PYDISTUTILS_SETUP} test

.include <bsd.port.mk>
