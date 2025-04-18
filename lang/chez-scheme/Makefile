# Created by: Ashish SHUKLA <ashish@FreeBSD.org>

PORTNAME=	chez-scheme
PORTVERSION=	9.5.4
DISTVERSIONPREFIX=	v
PORTREVISION=	2
CATEGORIES=	lang
MASTER_SITES=	http://distfiles.pirateparty.in/ashish/:boot \
		LOCAL/ashish:boot
DISTFILES=	${PORTNAME}-boot-ta6fb-${PORTVERSION}.tar.xz:boot \
		${PORTNAME}-boot-ti3fb-${PORTVERSION}.tar.xz:boot

MAINTAINER=	ashish@FreeBSD.org
COMMENT=	Chez Scheme system

LICENSE=	APACHE20
LICENSE_FILE=	${WRKSRC}/LICENSE

ONLY_FOR_ARCHS=	amd64 i386

LIB_DEPENDS=	libuuid.so:misc/e2fsprogs-libuuid \
		libossp-uuid.so:misc/ossp-uuid

USES=		gmake iconv:lib ncurses
USE_GITHUB=	yes
GH_ACCOUNT=	cisco
GH_PROJECT=	ChezScheme
GH_TUPLE=	nanopass:nanopass-framework-scheme:v1.9.1:nanopass/nanopass \
		madler:zlib:v1.2.11:zlib/zlib \
		dybvig:stex:v1.2.2:stex/stex \
		lz4:lz4:3d67671:lz4/lz4

OPTIONS_DEFAULT=	X11
OPTIONS_DEFINE=	X11

HAS_CONFIGURE=	yes
ALL_TARGET=	build
CONFLICTS_INSTALL=	petite-chez
STRIP_FILES=	bin/petite bin/${PORTNAME} bin/${PORTNAME}-script
CHEZ_LIBDIR=lib/csv${PORTVERSION}
CFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib -luuid
CONFIGURE_ARGS=	--installprefix=${PREFIX} \
		--temproot=${STAGEDIR} \
		--installschemename=${PORTNAME} \
		--installscriptname=${PORTNAME}-script
PLIST_SUB=	PORTNAME=${PORTNAME} \
		CHEZ_ARCH=${CHEZ_ARCH} \
		CHEZ_LIBDIR=${CHEZ_LIBDIR}
X11_USES=	xorg
X11_USE=	XORG=x11

.include <bsd.port.pre.mk>

.if (${ARCH} == "amd64")
CONFIGURE_ARGS+=	--threads --64 -m=ta6fb
CHEZ_ARCH=	ta6fb
.elif (${ARCH} == "i386")
CONFIGURE_ARGS+=	--threads --32 -m=ti3fb
CHEZ_ARCH=	ti3fb
.endif

post-patch:
	${LN} -sf ${WRKDIR}/${CHEZ_ARCH} ${WRKSRC}/boot/
	${REINPLACE_CMD} -e 's,/usr/X11R6,${LOCALBASE},g' \
		-e 's,/usr/local,${LOCALBASE},g' \
		-e 's,-liconv,${ICONV_LIB},g' ${WRKSRC}/c/Mf-${CHEZ_ARCH}

pre-build-X11-off:
	${ECHO_CMD} '#undef LIBX11' >>${WRKSRC}/c/version.h

post-install:
.for f in ${STRIP_FILES}
	@${CHMOD} +w ${STAGEDIR}${PREFIX}/${f}
	@${STRIP_CMD} ${STAGEDIR}${PREFIX}/${f}
	@${CHMOD} -w ${STAGEDIR}${PREFIX}/${f}
.endfor
	@${LN} -sf scheme.boot ${STAGEDIR}${PREFIX}/${CHEZ_LIBDIR}/${CHEZ_ARCH}/${PORTNAME}-script.boot

.include <bsd.port.post.mk>
