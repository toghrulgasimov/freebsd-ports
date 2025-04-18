PORTNAME=	eaglemode
PORTVERSION=	0.95.0
PORTREVISION=	18
CATEGORIES=	x11
MASTER_SITES=	SF/${PORTNAME}/${PORTNAME}-${PORTVERSION}

MAINTAINER=	amdmi3@FreeBSD.org
COMMENT=	Futuristic zoomable user environment

LICENSE=	GPLv3

LIB_DEPENDS=	libpng.so:graphics/png \
		libtiff.so:graphics/tiff \
		libfreetype.so:print/freetype2

USES=		compiler:features jpeg gnome perl5 \
		pkgconfig tar:bzip2 xorg
USE_PERL5=	build
USE_XORG=	x11 xext xxf86vm
SUB_FILES=	eaglemode.sh

LLD_UNSAFE=	yes

BUILD_ARGS=	continue=no

.for lib in X11 jpeg png tiff
BUILD_ARGS+=	${lib}-inc-dir="${LOCALBASE}/include" \
		${lib}-lib-dir="${LOCALBASE}/lib"
.endfor

DATADIR=	${PREFIX}/lib/${PORTNAME}
PLIST_FILES=	bin/${PORTNAME}
PORTDATA=	*

OPTIONS_DEFINE=	RSVG PDF
OPTIONS_DEFAULT=VLC RSVG PDF
OPTIONS_SUB=	yes
OPTIONS_GROUP=	EMAV
OPTIONS_GROUP_EMAV=	XINE VLC

RSVG_DESC=	SVG support through librsvg
PDF_DESC=	PDF support through poppler-glib
EMAV_DESC=	Video preview backend
VLC_DESC=	Multimedia support via VLC

XINE_LIB_DEPENDS=	libxine.so:multimedia/libxine
XINE_VARS=		EMAV+=xine
RSVG_USE=		GNOME=librsvg2
PDF_LIB_DEPENDS=	libpoppler-glib.so:graphics/poppler-glib
PDF_USE=		GNOME=gtk20
VLC_LIB_DEPENDS=	libvlc.so:multimedia/vlc
VLC_VARS=		EMAV+=vlc

.include <bsd.port.pre.mk>

.if ${COMPILER_TYPE} == gcc && ${COMPILER_VERSION} <= 42
USE_GCC=	yes
.endif

.if ${PORT_OPTIONS:MXINE}
BUILD_ARGS+=	xine-inc-dir="${LOCALBASE}/include" \
		xine-lib-dir="${LOCALBASE}/lib"
.endif
.if !empty(EMAV)
BUILD_ARGS+=	emAv=${EMAV:ts,}
.endif

post-patch:
	@${FIND} ${WRKSRC} -name "*.pl" | ${XARGS} \
		${REINPLACE_CMD} -e '1s|/usr/bin/perl|${perl_CMD}|'
.if empty(EMAV)
	@${RM} ${WRKSRC}/makers/emAv.maker.pm
.endif

post-patch-RSVG-off:
	@${RM} ${WRKSRC}/makers/emSvg.maker.pm

post-patch-PDF-off:
	@${RM} ${WRKSRC}/makers/emPdf.maker.pm

do-build:
	@(cd ${WRKSRC} && ${SETENV} ${MAKE_ENV} \
		${PERL} make.pl build ${BUILD_ARGS})

do-install:
	@${MKDIR} ${STAGEDIR}${DATADIR}
	cd ${WRKSRC} && ${PERL} make.pl install dir=${STAGEDIR}${DATADIR}
	${INSTALL_SCRIPT} ${WRKDIR}/eaglemode.sh ${STAGEDIR}${PREFIX}/bin/eaglemode
	@${STRIP_CMD} ${STAGEDIR}${PREFIX}/lib/eaglemode/bin/* \
		${STAGEDIR}${PREFIX}/lib/eaglemode/lib/*.so \
		${STAGEDIR}${PREFIX}/lib/eaglemode/lib/emClock/emTimeZonesProc \
		${STAGEDIR}${PREFIX}/lib/eaglemode/lib/emTmpConv/emTmpConvProc

do-install-XINE-on:
	@${STRIP_CMD} ${STAGEDIR}${PREFIX}/lib/eaglemode/lib/emAv/emAvServerProc_xine

do-install-VLC-on:
	@${STRIP_CMD} ${STAGEDIR}${PREFIX}/lib/eaglemode/lib/emAv/emAvServerProc_vlc

do-install-RSVG-on:
	@${STRIP_CMD} ${STAGEDIR}${PREFIX}/lib/eaglemode/lib/emSvg/emSvgServerProc

do-install-PDF-on:
	@${STRIP_CMD} ${STAGEDIR}${PREFIX}/lib/eaglemode/lib/emPdf/emPdfServerProc

.include <bsd.port.post.mk>
