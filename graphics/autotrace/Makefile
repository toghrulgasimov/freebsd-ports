# Created by: KANOU Hiroki <kanou@mil.allnet.ne.jp>

PORTNAME=	autotrace
PORTVERSION=	0.31.1
PORTREVISION=	32
CATEGORIES=	graphics
MASTER_SITES=	SF/${PORTNAME}/AutoTrace/${PORTVERSION}

MAINTAINER=	portmaster@BSDforge.com
COMMENT=	Convert bitmap to vector graphics

LICENSE=	GPLv2 LGPL21
LICENSE_COMB=	multi

LIB_DEPENDS=	libpng.so:graphics/png

USES=		cpe pathfix pkgconfig libtool
CPE_VENDOR=	autotrace_project
GNU_CONFIGURE=	yes
USE_LDCONFIG=	yes
CPPFLAGS+=	$$(libpng-config --I_opts)
LDFLAGS+=	$$(libpng-config --L_opts)
INSTALL_TARGET=	install-strip

OPTIONS_DEFINE=	IMAGEMAGICK MING PSTOEDIT
OPTIONS_DEFAULT=IMAGEMAGICK
MING_DESC=	Enable swf interface
PSTOEDIT_DESC=	Convert postscript to other formats

IMAGEMAGICK_USES=		magick:6
IMAGEMAGICK_CONFIGURE_OFF=	--without-magick

MING_LIB_DEPENDS=	libming.so:graphics/ming
MING_CPPFLAGS=		-I${LOCALBASE}/include -I${LOCALBASE}/include/ming
MING_CONFIGURE_OFF=	ac_cv_header_ming_h=no

PSTOEDIT_LIB_DEPENDS=	libpstoedit.so:graphics/pstoedit
PSTOEDIT_CONFIGURE_OFF=	--without-pstoedit

post-patch:
	@${REINPLACE_CMD} -e \
		's|Magick-config|MagickWand-config|g ; \
		/$$PSTOEDIT_CONFIG/s|--version|--modversion| ; \
		s|$$PSTOEDIT_CONFIG $$pstoedit_args|pkg-config pstoedit| ; \
		/^PSTOEDIT_CONFIG=/s|=.*$$|=pkg-config|' ${WRKSRC}/configure

post-install:
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/lib/libautotrace.so

.include <bsd.port.mk>
