# Created by: kwm@FreeBSD.org

PORTNAME=	wayland
DISTVERSION=	1.20.0
CATEGORIES=	graphics wayland
MASTER_SITES=	https://wayland.freedesktop.org/releases/

MAINTAINER=	x11@FreeBSD.org
COMMENT=	Wayland composite "server"

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/COPYING

LIB_DEPENDS=	libexpat.so:textproc/expat2 \
		libffi.so:devel/libffi \
		libepoll-shim.so:devel/libepoll-shim

USES=		cpe gnome meson pkgconfig tar:xz
USE_GNOME=	libxslt:build
USE_LDCONFIG=	yes
MESON_ARGS=	-Ddocumentation=false

.include <bsd.port.mk>
