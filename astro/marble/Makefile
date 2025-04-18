PORTNAME=	marble
DISTVERSION=	${KDE_APPLICATIONS_VERSION}
PORTREVISION=	2
CATEGORIES=	astro education kde kde-applications

MAINTAINER=	kde@FreeBSD.org
COMMENT=	Virtual globe and world atlas for KDE

LICENSE=	GPLv2+
LICENSE_FILE=	${WRKSRC}/LICENSE.txt

LIB_DEPENDS=	libquazip1-qt5.so:archivers/quazip

USES=		cmake compiler:c++11-lang desktop-file-utils gettext \
		kde:5 qt:5 shared-mime-info tar:xz
USE_KDE=	attica auth codecs completion config configwidgets coreaddons \
		crash doctools i18n jobwidgets kio newstuff package parts \
		plasma-framework plasma-workspace-wallpapers runner service solid \
		sonnet textwidgets wallet widgetsaddons windowsystem xmlgui \
		ecm_build
USE_QT=		concurrent core dbus declarative designer gui location network opengl \
		phonon4 printsupport script serialport sql svg webchannel widgets xml \
		buildtools_build qmake_build testlib_build

USE_LDCONFIG=	yes
MAKE_ENV=	XDG_CONFIG_HOME=/dev/null
# We have to set QT_IMPORTS_PATH, as it does not get picked up
CMAKE_ARGS=	-DMOBILE:BOOL=FALSE \
		-DQT_IMPORTS_DIR:PATH=${QT_IMPORTDIR}

# Override shared library version
KDE_APPLICATIONS_SHLIB_VER=	21.4.0

OPTIONS_DEFINE=	GPS DOCS WEBENGINE
OPTIONS_DEFAULT=GPS
OPTIONS_DEFAULT_amd64=	WEBENGINE
OPTIONS_DEFAULT_i386=	WEBENGINE
OPTIONS_SUB=	yes

GPS_DESC=		Support for GPS position provider
GPS_LIB_DEPENDS=	libgps.so:astro/gpsd
GPS_CMAKE_BOOL_OFF=	CMAKE_DISABLE_FIND_PACKAGE_libgps

WEBENGINE_DESC=		Add dependency on qt5-webengine
WEBENGINE_USE=		QT=webengine
WEBENGINE_CMAKE_BOOL_OFF=	CMAKE_DISABLE_FIND_PACKAGE_Qt5WebEngineWidgets

.include <bsd.port.options.mk>
.if ${PORT_OPTIONS:MWEBENGINE}
DEPRECATED=	Uses EOL Python 2.7 via www/qt5-webengine
EXPIRATION_DATE=2021-06-23
.endif

.include <bsd.port.mk>
