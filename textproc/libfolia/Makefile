PORTNAME=	libfolia
DISTVERSIONPREFIX=	v
DISTVERSION=	2.10
CATEGORIES=	textproc

MAINTAINER=	yuri@FreeBSD.org
COMMENT=	Library for FoLiA, a format for annotated language resources

LICENSE=	APACHE20
LICENSE_FILE=	${WRKSRC}/COPYING

BUILD_DEPENDS=	autoconf-archive>=0:devel/autoconf-archive
LIB_DEPENDS=	libicui18n.so:devel/icu \
		libticcutils.so:devel/ticcutils

USES=		autoreconf compiler:c++11-lang gmake gnome libtool pkgconfig
USE_GNOME=	libxml2
USE_LDCONFIG=	yes

GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--disable-static

USE_GITHUB=	yes
GH_ACCOUNT=	LanguageMachines

INSTALL_TARGET=	install-strip

.include <bsd.port.mk>
