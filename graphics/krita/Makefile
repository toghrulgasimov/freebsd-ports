PORTNAME=	krita
DISTVERSION=	4.4.8
PORTREVISION=	4
CATEGORIES=	graphics kde
MASTER_SITES=	KDE/stable/${PORTNAME}/${DISTVERSION}
DIST_SUBDIR=	KDE/${PORTNAME}

MAINTAINER=	kde@FreeBSD.org
COMMENT=	Sketching and painting program

LICENSE=	GPLv2
LICENSE_FILE=	${WRKSRC}/COPYING

LIB_DEPENDS=	libImath.so:math/Imath \
		libOpenColorIO.so:graphics/opencolorio \
		libX11.so:x11/libX11 \
		libboost_system.so:devel/boost-libs \
		libfftw3.so:math/fftw3 \
		libexiv2.so:graphics/exiv2 \
		libcurl.so:ftp/curl \
		libgif.so:graphics/giflib \
		libgsl.so:math/gsl \
		libheif.so:graphics/libheif \
		liblcms2.so:graphics/lcms2 \
		libpng.so:graphics/png \
		libpoppler.so:graphics/poppler \
		libpoppler-qt5.so:graphics/poppler-qt5 \
		libquazip1-qt5.so:archivers/quazip \
		libraw.so:graphics/libraw \
		libtiff.so:graphics/tiff \
		libxcb.so:x11/libxcb \
		libxcb-util.so:x11/xcb-util

# Disable ninja generator for now (with gmake), until the duplicate test targets are resolved upstream.
USES=		cmake:noninja gmake compiler:c++11-lib desktop-file-utils \
		eigen:3 gettext jpeg kde:5 pkgconfig python:3.4+ qt:5 \
		shared-mime-info tar:xz xorg
USE_KDE=	archive completion config coreaddons crash guiaddons i18n \
		itemmodels itemviews kio service widgetsaddons windowsystem
USE_QT=		concurrent core dbus declarative gui multimedia network printsupport \
		svg testlib widgets x11extras xml \
		buildtools_build qmake_build
USE_XORG=	ice sm xcb xext xi

CMAKE_ARGS=	-DCMAKE_DISABLE_FIND_PACKAGE_PyQt5:BOOL=true

OPTIONS_DEFINE=		GMIC OPENEXR
OPTIONS_DEFAULT=	OPENEXR
OPTIONS_SUB=		yes

GMIC_DESC=		Depend on the G'Mic plugin #'
GMIC_RUN_DEPENDS=	gmic_krita_qt:graphics/gmic-qt@krita

OPENEXR_LIB_DEPENDS=	libOpenEXR.so:graphics/openexr \
			libSeExpr2.so:graphics/seexpr
OPENEXR_CMAKE_BOOL_OFF=	CMAKE_DISABLE_FIND_PACKAGE_OpenEXR

CONFLICTS_INSTALL=	calligra-2*

PLIST_SUB=	SHLIB_VER=20.0.0 \
		SHLIB_SHVER=20

CFLAGS+=	-I${LOCALBASE}/include/Imath
LDFLAGS+=	-lpthread

.include <bsd.port.mk>
