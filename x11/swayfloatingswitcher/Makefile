PORTNAME=	swayfloatingswitcher
PORTVERSION=	s20211208
CATEGORIES=	x11

MAINTAINER=	jbeich@FreeBSD.org
COMMENT=	Simple Alt+Tab switcher for floating windows

LICENSE=	GPLv3+
LICENSE_FILE=	${WRKSRC}/LICENSE

BUILD_DEPENDS=	valac:lang/vala \
		granite>0:x11-toolkits/granite
LIB_DEPENDS=	libjson-glib-1.0.so:devel/json-glib \
		libgee-0.8.so:devel/libgee \
		libgtk-layer-shell.so:x11-toolkits/gtk-layer-shell

USES=		gnome localbase:ldflags meson pkgconfig
USE_GITHUB=	yes
USE_GNOME=	gtk30
GH_ACCOUNT=	ErikReider
GH_PROJECT=	SwayFloatingSwitcher
GH_TAGNAME=	4f02259
PLIST_FILES=	bin/${PORTNAME} \
		bin/${PORTNAME}-client

.include <bsd.port.mk>
