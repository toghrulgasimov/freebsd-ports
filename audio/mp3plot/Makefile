# Created by: Andrew Pantyukhin <infofarmer@FreeBSD.org>

PORTNAME=	mp3plot
DISTVERSION=	0.6.0
PORTREVISION=	29
CATEGORIES=	audio
MASTER_SITES=	http://p.outlyer.net/mp3plot/files/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	MP3 bitrate plot tool

LICENSE=	GPLv2
LICENSE_FILE=	${WRKSRC}/COPYING

USES=		compiler:c++11-lang
LIB_DEPENDS=	libboost_thread.so:devel/boost-libs

USE_CXXSTD=	c++98

OPTIONS_DEFINE=	GD IMAGEMAGICK
OPTIONS_DEFAULT=GD

CONFIGURE_ARGS=	--with-boost-program-options=boost_program_options \
		--with-boost-thread=boost_thread
CPPFLAGS+=	-I${LOCALBASE}/include
GNU_CONFIGURE=	yes
LIBS+=		-L${LOCALBASE}/lib -lboost_system

PLIST_FILES=	bin/${PORTNAME} man/man1/${PORTNAME}.1.gz

GD_CONFIGURE_ENABLE=	gd
GD_LIB_DEPENDS=		libgd.so:graphics/gd
IMAGEMAGICK_CONFIGURE_ENABLE=	magick
IMAGEMAGICK_USES=	magick:6

post-patch:
	@${REINPLACE_CMD} -e '/bldtype_/s|-O2||g; s|^extra_LD.*||g' ${WRKSRC}/configure

.include <bsd.port.mk>
