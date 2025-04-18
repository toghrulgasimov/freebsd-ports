# Created by: Yinghong.Liu <relaxbsd@gmail.com>

PORTNAME=	synfig
PORTVERSION=	1.2.2
DISTVERSIONPREFIX=v
PORTREVISION=	17
CATEGORIES=	graphics devel multimedia

MAINTAINER=	portmaster@BSDforge.com
COMMENT=	Vector based 2D animation package

LICENSE=	GPLv2+

BUILD_DEPENDS=	etl>=1.2.2:devel/etl \
		gsed:textproc/gsed
LIB_DEPENDS=	libImath.so:math/Imath \
		libOpenEXR.so:graphics/openexr \
		libavcodec.so:multimedia/ffmpeg \
		libboost_program_options.so:devel/boost-libs \
		libdv.so:multimedia/libdv \
		libfftw3.so:math/fftw3 \
		libfontconfig.so:x11-fonts/fontconfig \
		libfreetype.so:print/freetype2 \
		libltdl.so:devel/libltdl \
		libmng.so:graphics/libmng \
		libpng.so:graphics/png \
		libtiff.so:graphics/tiff

PORTSCOUT=	limitw:1,even

USES=		autoreconf compiler:c++11-lang gmake gnome iconv jpeg \
		libtool localbase magick:6 mlt:6 pathfix pkgconfig
USE_CXXSTD=	c++11
USE_GITHUB=	yes
USE_GNOME=	cairo glibmm intltool libxml++26 pango
GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	${ICONV_CONFIGURE_ARG}
CONFIGURE_ENV+=	ac_cv_path_SED=${LOCALBASE}/bin/gsed
# Other spurious uses of direct sed have popped up
BINARY_ALIAS=	sed=${LOCALBASE}/bin/gsed
INSTALL_TARGET=	install-strip
USE_LDCONFIG=	yes
WRKSRC_SUBDIR=	synfig-core

OPTIONS_DEFINE=	DOCS NLS
OPTIONS_SUB=	yes

NLS_USES=		gettext
NLS_CONFIGURE_ENABLE=	nls

post-install:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
.for doc in AUTHORS NEWS README TODO
	(cd ${WRKSRC} &&  ${INSTALL_DATA} ${doc} ${STAGEDIR}${DOCSDIR})
.endfor

.include <bsd.port.mk>
