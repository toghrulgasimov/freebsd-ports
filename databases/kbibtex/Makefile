# Created by: Markus Brueffer <markus@FreeBSD.org>

PORTNAME=	kbibtex
DISTVERSION=	0.9.2
PORTREVISION=	24
CATEGORIES=	databases kde
MASTER_SITES=	KDE/stable/KBibTeX/${DISTVERSION}

MAINTAINER=	kde@FreeBSD.org
COMMENT=	Bibliography editor for KDE

LIB_DEPENDS=	libicuuc.so:devel/icu \
		libpoppler.so:graphics/poppler \
		libpoppler-qt5.so:graphics/poppler-qt5 \
		libqoauth-qt5.so:net/qoauth-qt5

USES=		cmake compiler:c++11-lang desktop-file-utils gettext gnome \
		iconv kde:5 qca qt:5 shared-mime-info tar:xz
USE_GNOME=	libxml2 libxslt
USE_KDE=	auth bookmarks codecs completion config configwidgets \
		coreaddons crash ecm i18n iconthemes itemviews jobwidgets \
		kio parts service solid sonnet texteditor textwidgets wallet \
		widgetsaddons windowsystem xmlgui \
		doctools_build
USE_QT=		concurrent core dbus declarative gui location network \
		printsupport webchannel widgets xml xmlpatterns \
		buildtools_build qmake_build
USE_LDCONFIG=	yes

OPTIONS_DEFINE=	WEBENGINE
OPTIONS_DEFAULT_amd64=	WEBENGINE
OPTIONS_DEFAULT_i386=	WEBENGINE

WEBENGINE_DESC=		Add dependency on qt5-webengine
WEBENGINE_USE=		QT=webengine
WEBENGINE_USE_OFF=	QT=webkit
WEBENGINE_CMAKE_BOOL_OFF=	CMAKE_DISABLE_FIND_PACKAGE_Qt5WebEngineWidgets

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MWEBENGINE}
DEPRECATED=	Uses EOL Python 2.7 via www/qt5-webengine
EXPIRATION_DATE=2021-06-23
.endif

.include <bsd.port.mk>
