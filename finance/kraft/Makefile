PORTNAME=	kraft
DISTVERSIONPREFIX=	v
DISTVERSION=	0.97
CATEGORIES=	finance kde

PATCH_SITES=	https://github.com/dragotin/kraft/commit/
PATCHFILES=	14906b37cd58136b8f16592e6f62ac147c3e2e71.patch:-p1

MAINTAINER=	kde@FreeBSD.org
COMMENT=	Manage invoices and documents for small companies

LICENSE=	GPLv2+
LICENSE_FILE=	${WRKSRC}/COPYING

BUILD_DEPENDS=	bash:shells/bash
LIB_DEPENDS=	libctemplate.so:textproc/google-ctemplate

USES=		cmake compiler:c++11-lang grantlee:5 kde:5 qt:5 shebangfix
USE_KDE=	akonadi akonadicontacts \
		auth codecs config configwidgets contacts coreaddons \
		i18n itemmodels widgetsaddons
USE_QT=		core dbus gui sql widgets xml \
		buildtools_build qmake_build

SHEBANG_FILES=	manual/makeman.sh

USE_GITHUB=	yes
GH_ACCOUNT=	dragotin

.include <bsd.port.mk>
