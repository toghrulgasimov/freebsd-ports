PORTNAME=	kitinerary
DISTVERSION=	${KDE_APPLICATIONS_VERSION}
PORTREVISION=	4
CATEGORIES=	net kde kde-applications

MAINTAINER=	kde@FreeBSD.org
COMMENT=	Data Model and Extraction System for Travel Reservation information

LICENSE=	LGPL21

LIB_DEPENDS=	libphonenumber.so:devel/libphonenumber \
		libpoppler.so:graphics/poppler \
		libZXing.so:textproc/zxing-cpp

USES=		compiler:c++11-lang cmake gettext gnome kde:5 pkgconfig qt:5 \
		shared-mime-info ssl tar:xz
USE_GNOME=	libxml2
USE_KDE=	archive coreaddons i18n \
		ecm_build
# Pim components
USE_KDE+=	calendarcore contacts kpkpass mime
USE_QT=		core declarative gui network \
		buildtools_build qmake_build
USE_LDCONFIG=	yes

DESCR=		${.CURDIR:H:H}/deskutils/kdepim/pkg-descr

OPTIONS_DEFINE=	DOCS

.include <bsd.port.mk>
