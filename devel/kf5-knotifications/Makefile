PORTNAME=	knotifications
DISTVERSION=	${KDE_FRAMEWORKS_VERSION}
PORTREVISION=	1
CATEGORIES=	devel kde kde-frameworks

MAINTAINER=	kde@FreeBSD.org
COMMENT=	KF5 abstraction for system notifications

LIB_DEPENDS=	libdbusmenu-qt5.so:devel/libdbusmenu-qt \
		libcanberra.so:audio/libcanberra

USES=		cmake compiler:c++11-lib gettext kde:5 qt:5 tar:xz xorg
USE_KDE=	codecs config coreaddons windowsystem \
		ecm_build
USE_QT=		core dbus declarative gui linguisttools network phonon4 widgets x11extras \
		buildtools_build qmake_build
USE_XORG=	x11 xtst

OPTIONS_DEFINE=		AUDIO
OPTIONS_DEFAULT=	AUDIO

AUDIO_DESC=		Audio notifications/text-to-speech support
AUDIO_LIB_DEPENDS=	libcanberra-gtk3.so:audio/libcanberra-gtk3
AUDIO_USE=		QT=speech
AUDIO_USES=		pkgconfig

.include <bsd.port.mk>
