PORTNAME=	libkdegames
DISTVERSION=	${KDE_APPLICATIONS_VERSION}
PORTREVISION=	1
CATEGORIES=	games kde kde-applications

MAINTAINER=	kde@FreeBSD.org
COMMENT=	Libraries used by KDE games

LIB_DEPENDS=	libsndfile.so:audio/libsndfile

USES=		cmake compiler:c++11-lang gettext kde:5 openal qt:5 \
		tar:xz
USE_KDE=	archive attica auth bookmarks codecs completion config \
		configwidgets coreaddons crash dbusaddons dnssd emoticons \
		globalaccel guiaddons i18n iconthemes init itemmodels \
		itemviews jobwidgets kdeclarative kdelibs4support kio newstuff \
		package service textwidgets widgetsaddons xmlgui \
		ecm_build
USE_QT=		core dbus declarative gui network svg widgets xml \
		buildtools_build qmake_build testlib_build
USE_LDCONFIG=	yes

SHLIB_VER=	7.0.0
PLIST_SUB+=	SHLIB_VER="${SHLIB_VER}" \
		SHLIB_SHVER="${SHLIB_VER:R:R}"

OPTIONS_DEFINE=	DOCS

.include <bsd.port.mk>
