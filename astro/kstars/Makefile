PORTNAME=	kstars
DISTVERSION=	3.5.6
PORTEPOCH=	1
CATEGORIES=	astro kde
MASTER_SITES=	KDE/stable/${PORTNAME}

MAINTAINER=	kde@FreeBSD.org
COMMENT=	KDE desktop planetarium

LICENSE=	GPLv2

LIB_DEPENDS=	libcfitsio.so:astro/cfitsio \
		libindidriver.so:devel/indi \
		libqt5keychain.so:security/qtkeychain \
		libraw.so:graphics/libraw \
		libsecret-1.so:security/libsecret \
		libstellarsolver.so:astro/stellarsolver \
		libwcs.so:astro/wcslib
BUILD_DEPENDS=	xplanet:astro/xplanet
RUN_DEPENDS=	xplanet:astro/xplanet

USES=		cmake compiler:c++11-lib desktop-file-utils eigen:3 \
		gettext gnome kde:5 localbase:ldflags pkgconfig qt:5 tar:xz
USE_GNOME=	glib20
USE_KDE=	attica auth bookmarks codecs completion config configwidgets\
		coreaddons crash dbusaddons guiaddons i18n \
		iconthemes init itemviews jobwidgets kio newstuff notifications \
		notifyconfig parts plotting service solid texteditor \
		widgetsaddons xmlgui \
		doctools_build ecm_build
USE_QT=		concurrent core datavis3d dbus declarative gui multimedia \
		network opengl printsupport sql svg testlib websockets widgets \
		xml \
		buildtools_build qmake_build

post-extract:
	# KDE Bug https://bugs.kde.org/show_bug.cgi?id=439541
	${RM} ${WRKSRC}/po/de/docs/kstars/index.docbook

.include <bsd.port.mk>
