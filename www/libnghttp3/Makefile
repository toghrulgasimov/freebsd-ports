# Created by: Po-Chuan Hsieh <sunpoet@FreeBSD.org>

PORTNAME=	nghttp3
PORTVERSION=	0.1.0.g20211117
CATEGORIES=	www net
PKGNAMEPREFIX=	lib

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	HTTP/3 C Library

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/COPYING

USES=		autoreconf compiler:c++17-lang libtool pathfix pkgconfig

CONFIGURE_ARGS=	--enable-lib-only
GNU_CONFIGURE=	yes
INSTALL_TARGET=	install-strip
USE_CXXSTD=	c++17
USE_LDCONFIG=	yes

GH_ACCOUNT=	ngtcp2
GH_TAGNAME=	b9e565c
USE_GITHUB=	yes

post-patch:
	@${REINPLACE_CMD} -e 's|%%PORTVERSION%%|${PORTVERSION}|' ${WRKSRC}/configure.ac

.include <bsd.port.mk>
