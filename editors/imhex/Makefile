PORTNAME=	imhex
PORTVERSION=	1.12.1
DISTVERSIONPREFIX=	v
CATEGORIES=	editors
MASTER_SITES=	https://git.sr.ht/~danyspin97/xdgpp/blob/f01f810714443d0f10c333d4d1d9c0383be41375/:xdg
DISTFILES=	xdg.hpp:xdg
DIST_SUBDIR=	imhex

MAINTAINER=	nobutaka@FreeBSD.org
COMMENT=	Hex editor for reverse engineers and programmers

LICENSE=	GPLv2
LICENSE_FILE=	${WRKSRC}/LICENSE

NOT_FOR_ARCHS=	i386 powerpc
NOT_FOR_ARCHS_REASON=	__uint128_t and __int128_t are not supported
EXTRACT_ONLY=	${DISTNAME}${EXTRACT_SUFX} \
		btzy-nativefiledialog-extended-${GH_TAG_NATIVEFILEDIALOG}_GH0${EXTRACT_SUFX} \
		fmtlib-fmt-${GH_TAG_FMT}_GH0${EXTRACT_SUFX}

BUILD_DEPENDS=	glm>0:math/glm \
		nlohmann-json>0:devel/nlohmann-json \
		${LOCALBASE}/include/range/v3/range.hpp:devel/range-v3
LIB_DEPENDS=	libcapstone.so:devel/capstone4 \
		libcurl.so:ftp/curl \
		libfreetype.so:print/freetype2 \
		libglfw.so:graphics/glfw \
		libharfbuzz.so:print/harfbuzz \
		libmbedtls.so:security/mbedtls \
		libtre.so:textproc/libtre \
		libyara.so:security/yara

USES=		cmake gl gnome pkgconfig python:3.8+ xorg
USE_GL=		gl
USE_GNOME=	cairo gdkpixbuf2 gtk30
USE_XORG=	x11 xcb xau xdmcp
USE_GITHUB=	yes

GH_ACCOUNT=	WerWolv
GH_PROJECT=	ImHex
GH_TUPLE=	btzy:nativefiledialog-extended:${GH_TAG_NATIVEFILEDIALOG}:nativefiledialog \
		fmtlib:fmt:${GH_TAG_FMT}:fmt
GH_TAG_FMT=	d141cdb
GH_TAG_NATIVEFILEDIALOG=	322d1bc

CMAKE_ARGS=	-DUSE_SYSTEM_CAPSTONE=ON -DUSE_SYSTEM_CURL=ON -DUSE_SYSTEM_YARA=ON -DUSE_SYSTEM_NLOHMANN_JSON=ON

PORTDOCS=	README.md

OPTIONS_DEFINE=	DOCS NLS
NLS_USES=	gettext

post-extract:
	${CP} ${DISTDIR}/${DIST_SUBDIR}/xdg.hpp ${WRKSRC}/external/xdgpp
	${CP} -R ${WRKSRC_fmt}/* ${WRKSRC}/external/fmt
	${CP} -R ${WRKSRC_nativefiledialog}/* ${WRKSRC}/external/nativefiledialog

post-install-DOCS-on:
	${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/README.md ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
