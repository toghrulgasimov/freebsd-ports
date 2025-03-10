PORTNAME=	lepton-eda
PORTVERSION=	1.9.17
CATEGORIES=	cad
MASTER_SITES=	https://github.com/lepton-eda/lepton-eda/releases/download/${PORTVERSION}-20211219/

MAINTAINER=	graahnul.grom@gmail.com
COMMENT=	Lepton Electronic Design Automation

LICENSE=	GPLv2+

LIB_DEPENDS=	libfontconfig.so:x11-fonts/fontconfig \
		libfreetype.so:print/freetype2 \
		libgc-threaded.so:devel/boehm-gc-threaded \
		libguile-2.2.so:lang/guile2 \
		libpng.so:graphics/png \
		libstroke.so:devel/libstroke \
		libgtkextra-x11-3.0.so:x11-toolkits/gtkextra \
		libharfbuzz.so:print/harfbuzz \
		libffi.so:devel/libffi \
		libunistring.so:devel/libunistring \
		libgmp.so:math/gmp \
		libltdl.so:devel/libltdl \
		libfribidi.so:converters/fribidi \
		libpcre.so:devel/pcre \
		libgraphite2.so:graphics/graphite2 \
		libexpat.so:textproc/expat2 \
		libGLdispatch.so:graphics/libglvnd

USES=		desktop-file-utils gettext-tools gnome \
		groff:build libtool localbase makeinfo pathfix perl5 \
		pkgconfig shared-mime-info shebangfix iconv:wchar_t xorg
USE_XORG=	xrender xinerama xi xrandr xcursor xext x11 \
		xcomposite xdamage xfixes pixman xcb xau xdmcp
USE_GNOME=	cairo gtk20 gdkpixbuf2
USE_GL=	egl gl
USE_LDCONFIG=	yes

SHEBANG_FILES=	utils/pcb_backannotate/lepton-pcb_backannotate \
		utils/refdes_renum/lepton-refdes_renum \
		utils/symfix/lepton-symfix

GNU_CONFIGURE=	yes
INSTALL_TARGET=	install-strip

INFO=	lepton-scheme lepton-manual
PORTEXAMPLES=	examples/*

OPTIONS_DEFINE=	DOCS EXAMPLES NLS
OPTIONS_SUB=	yes

NLS_USES=		gettext-runtime
NLS_CONFIGURE_ENABLE=	nls

post-patch:
	${REINPLACE_CMD} -e \
		's,\$$(docdir)/examples,\$$(datadir)/examples/lepton-eda,' \
		${WRKSRC}/examples/Makefile.in \
		${WRKSRC}/examples/RF_Amp/Makefile.in \
		${WRKSRC}/examples/TwoStageAmp/Makefile.in \
		${WRKSRC}/examples/gTAG/Makefile.in \
		${WRKSRC}/examples/lightning_detector/Makefile.in

.include <bsd.port.mk>
