# Created by: Tobias Rehbein <tobias.rehbein@web.de>

PORTNAME=	stonesoup
PORTVERSION=	0.27.1
CATEGORIES=	games

MAINTAINER=	fuz@fuz.su
COMMENT=	Dungeon Crawl Stone Soup - a fun, free rogue-like game

LICENSE=	GPLv2
LICENSE_FILE=	${WRKSRC}/../../LICENSE

BUILD_DEPENDS=	${PYTHON_PKGNAMEPREFIX}yaml>0:devel/py-yaml@${PY_FLAVOR}

FLAVORS=	console sdl
FLAVOR?=	${FLAVORS[1]}
sdl_PKGNAMESUFFIX=	-sdl

USES=		bison compiler:c++11-lib gmake lua:51 perl5 pkgconfig \
		python:build shebangfix sqlite tar:xz

USE_GITHUB=	yes
GH_ACCOUNT=	crawl
GH_PROJECT=	crawl

USE_PERL5=	build
SHEBANG_FILES=	util/gen-mi-enum \
		util/good-depfile \
		util/species-gen.py \
		util/txc

DATADIR=	${PREFIX}/share/${PORTNAME}${PKGNAMESUFFIX}
SAVEDIR=	\~/.stonesoup
WRKSRC_SUBDIR=	crawl-ref/source
GAME=${PORTNAME}${PKGNAMESUFFIX}

SUB_FILES=	pkg-message
PLIST_SUB=	SAVEDIR="${SAVEDIR}" GAME="${GAME}" SDL=${"${FLAVOR}" == "sdl":?"":"@comment "}

MAKE_ARGS=	prefix=${PREFIX} \
		DATADIR=${DATADIR} \
		DESTDIR=${STAGEDIR} \
		FORCE_CC=${CC} \
		FORCE_CXX=${CXX} \
		GAME=${GAME} \
		INSTALL_UGRP=root:games \
		LUA_PACKAGE=lua-5.1 \
		NO_AUTO_OPT=YesPlease \
		NO_OPTIMIZE=YesPlease \
		NO_TRY_GOLD=YesPlease \
		POSIX=YesPlease \
		PYTHON=${PYTHON_CMD} \
		SAVEDIR=${SAVEDIR} \
		SQLITE_INCLUDE_DIR=${LOCALBASE}/include \
		SQLITE_LIB=-lsqlite3 \
		V=yes

OPTIONS_DEFINE=	LUA NOWIZARD SOUND
OPTIONS_DEFAULT=LUA
OPTIONS_SUB=	yes

SOUND_DESC=	Sound support
NOWIZARD_DESC=	Disable Wizard mode
LUA_DESC=	Bindings for LUA user scripts

.if ${FLAVOR} == sdl
USES+=		gl sdl
USE_SDL=	sdl2 image2 mixer2
USE_GL=		gl glu
MAKE_ARGS+=	TILES=y SOUND=y
BUILD_DEPENDS+=	\
		advpng:archivers/advancecomp \
		fc-list:x11-fonts/fontconfig \
		${LOCALBASE}/share/fonts/dejavu/DejaVuSans.ttf:x11-fonts/dejavu \
		pngcrush:graphics/pngcrush
RUN_DEPENDS+=	${LOCALBASE}/share/fonts/dejavu/DejaVuSans.ttf:x11-fonts/dejavu
LIB_DEPENDS+=libpng.so:graphics/png \
		libfreetype.so:print/freetype2
DESKTOP_ENTRIES=	"Dungeon Crawl Stone Soup" "${COMMENT}" "${DATADIR}/dat/tiles/stone_soup_icon-512x512.png" "${GAME}" "Game;" false
.else
USES+=		ncurses
.endif

NOWIZARD_MAKE_ARGS=	NOWIZARD=y
SOUND_MAKE_ARGS=	SOUND=y
SOUND_RUN_DEPENDS=	sox:audio/sox
LUA_MAKE_ARGS_OFF=	NO_LUA_BINDINGS=yes

post-patch-SOUND-on:
	@${REINPLACE_CMD} -e "s,%%LOCALBASE%%,${LOCALBASE}," ${WRKSRC}/sound.h
	@${REINPLACE_CMD} -e "s,%%SOUND%%,," ${WRKSRC}/sound.h

post-patch-SOUND-off:
	@${REINPLACE_CMD} -e "s,%%SOUND%%,// ," ${WRKSRC}/sound.h

pre-build:
	@${ECHO} ${PORTVERSION} > ${WRKSRC}/util/release_ver

pre-install:
	@${FIND} ${WRKSRC}/dat -type f -name '*.orig' -delete

post-install:
	@${RM} -r ${STAGEDIR}${DATADIR}/settings/mac

.include <bsd.port.mk>
