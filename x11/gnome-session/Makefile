# Created by: Joe Marcus Clarke <marcus@FreeBSD.org>

PORTNAME=	gnome-session
PORTVERSION=	40.1.1
CATEGORIES=	x11 gnome
MASTER_SITES=	GNOME/sources/${PORTNAME}/${PORTVERSION:C/^([0-9]+)\..*/\1/}
DIST_SUBDIR=	gnome

PATCH_SITES=	https://gitlab.gnome.org/GNOME/${PORTNAME}/-/commit/
PATCHFILES+=	1abd59271455.patch:-p1 # https://gitlab.gnome.org/GNOME/gnome-session/-/merge_requests/80

MAINTAINER=	gnome@FreeBSD.org
COMMENT=	Session component for the GNOME 3 desktop

LICENSE=	GPLv2+
LICENSE_FILE=	${WRKSRC}/COPYING

BUILD_DEPENDS=	xmlto:textproc/xmlto
LIB_DEPENDS=	libjson-glib-1.0.so:devel/json-glib \
		libdbus-glib-1.so:devel/dbus-glib \
		libepoxy.so:graphics/libepoxy
RUN_DEPENDS=	${LOCALBASE}/sbin/console-kit-daemon:sysutils/consolekit2 \
		dbus-daemon:devel/dbus

PORTSCOUT=	limitw:1,even

USES=		compiler:c11 gettext gl gnome localbase:ldflags meson \
		pkgconfig python:3.6+,build tar:xz xorg
USE_GNOME=	gnomedesktop3 gtk30
USE_XORG=	ice sm x11 xcomposite xtrans
USE_GL=		egl gl glesv2
MESON_ARGS=	-Dsystemd=false \
		-Dsystemd_session=disable \
		-Dsystemd_journal=false \
		-Dconsolekit=true
BINARY_ALIAS=	python3=${PYTHON_VERSION}

GLIB_SCHEMAS=	org.gnome.SessionManager.gschema.xml

.include <bsd.port.mk>
