# Created by: Koop Mast <kwm@FreeBSD.org>

PORTNAME=	gnome-calendar
PORTVERSION=	41.2
CATEGORIES=	deskutils gnome
MASTER_SITES=	GNOME/sources/${PORTNAME}/${PORTVERSION:C/^([0-9]+)\..*/\1/}
DIST_SUBDIR=	gnome

MAINTAINER=	gnome@FreeBSD.org
COMMENT=	Simple and beautiful calendar application for GNOME

LICENSE=	GPLv3
LICENSE_FILE=	${WRKSRC}/COPYING

BUILD_DEPENDS=	gsettings-desktop-schemas>=0:devel/gsettings-desktop-schemas
LIB_DEPENDS=	libical.so:devel/libical \
		libdazzle-1.0.so:x11-toolkits/libdazzle \
		libsoup-2.4.so:devel/libsoup \
		libgweather-3.so:net/libgweather \
		libgeoclue-2.so:net/geoclue \
		libgeocode-glib.so:net/geocode-glib \
		libgoa-1.0.so:net/gnome-online-accounts \
		libhandy-1.so:x11-toolkits/libhandy
RUN_DEPENDS=	gsettings-desktop-schemas>=0:devel/gsettings-desktop-schemas

PORTSCOUT=	limitw:1,even

USES=		compiler:c11 desktop-file-utils gettext gnome \
		localbase:ldflags meson pkgconfig python:3.4+,build tar:xz
USE_LDCONFIG=	yes
USE_GNOME=	cairo evolutiondataserver3 gtksourceview3
BINARY_ALIAS=	python3=${PYTHON_VERSION}

GLIB_SCHEMAS=	org.gnome.calendar.enums.xml \
		org.gnome.calendar.gschema.xml

.include <bsd.port.mk>
