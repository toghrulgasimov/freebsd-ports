PORTNAME=	pentobi
PORTVERSION=	19.1
CATEGORIES=	games
MASTER_SITES=	SF/${PORTNAME}/${PORTVERSION}

MAINTAINER=	amdmi3@FreeBSD.org
COMMENT=	Computer opponent for the board game Blokus

LICENSE=	GPLv3+
LICENSE_FILE=	${WRKSRC}/LICENSE.md

BUILD_DEPENDS=	itstool:textproc/itstool \
		xsltproc:textproc/libxslt \
		${LOCALBASE}/share/xsl/docbook/manpages/docbook.xsl:textproc/docbook-xsl

USES=		compiler:c++14-lang cmake desktop-file-utils gettext-tools gnome qt:5 \
		shared-mime-info tar:xz
USE_GNOME=	librsvg2:build
USE_QT=		core gui concurrent quickcontrols2 declarative network \
		qmake_build buildtools_build linguisttools_build
CMAKE_ARGS=	-DDOCBOOK_XSL=${LOCALBASE}/share/xsl/docbook/manpages/docbook.xsl

PORTDOCS=	AUTHORS.md HACKING.md NEWS.md README.md
PORTDATA=	*

OPTIONS_DEFINE=	DOCS TEST GNOME KDE
OPTIONS_DEFAULT=EXTERNAL_HELP
OPTIONS_SUB=	yes

TEST_CMAKE_BOOL=	PENTOBI_BUILD_TESTS
TEST_TEST_TARGET=	test
GNOME_DESC=		Build Gnome thumbnailer
GNOME_CMAKE_BOOL=	PENTOBI_BUILD_THUMBNAILER
KDE_CMAKE_BOOL=		PENTOBI_BUILD_KDE_THUMBNAILER
KDE_USES=		kde:5
KDE_USE=		KDE=kio
KDE_DESC=		Build KDE thumbnailer

post-install-DOCS-on:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	cd ${WRKSRC} && ${INSTALL_DATA} ${PORTDOCS} ${STAGEDIR}${DOCSDIR}/

.include <bsd.port.mk>
