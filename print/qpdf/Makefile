# Created by: Dmitry Kazarov <d.y.kazarov@mail.ru>

PORTNAME=	qpdf
DISTVERSION=	10.5.0
CATEGORIES=	print
MASTER_SITES=	SF

MAINTAINER=	wen@FreeBSD.org
COMMENT=	Command-line tools for transforming and inspecting PDF documents

LICENSE=	ART20 APACHE20
LICENSE_COMB=	dual
LICENSE_FILE_ART20=	${WRKSRC}/Artistic-2.0
LICENSE_FILE_APACHE20=	${WRKSRC}/LICENSE.txt

USES=		compiler:c++11-lang cpe gmake jpeg libtool localbase
GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--disable-static
USE_LDCONFIG=	yes
CPE_VENDOR=	qpdf_project

OPTIONS_DEFINE=	DOCS

.include <bsd.port.mk>
