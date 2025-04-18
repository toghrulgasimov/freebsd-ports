# Created by: hrs

PORTNAME=	alliance
DISTVERSION=	5.1.1
PORTREVISION=	2
CATEGORIES=	cad
MASTER_SITES=	ftp://asim.lip6.fr/pub/alliance/distribution/5.0/ \
		ftp://ftp.lyx.org/lip6/softs/alliance/distribution/5.0/ \
		ftp://ftp.jussieu.fr/lip6/softs/alliance/distribution/5.0/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Complete set of CAD tools and libraries for VLSI design

LICENSE=	Alliance
LICENSE_NAME=	Alliance VLSI Cad System License
LICENSE_FILE=	${WRKSRC}/LICENCE
LICENSE_PERMS=	dist-mirror dist-sell pkg-mirror pkg-sell auto-accept

BROKEN_aarch64=	fails to link: collect2: error: ld returned 1 exit status

BUILD_DEPENDS=	fig2dev:print/fig2dev

USES=		autoreconf:build gmake libtool magick:build motif tar:bz2 xorg
USE_GCC=	yes
USE_TEX=	dvipsk:build latex:build
USE_XORG=	ice sm x11 xext xt

HAS_CONFIGURE=	yes
CONFIGURE_ENV+=	ALLIANCE_TOP=${ALLIANCE_TOP} YACC=${YACC}
CONFIGURE_ARGS+=--mandir=${MANPREFIX}/man \
		--prefix=${ALLIANCE_TOP}

MAKE_JOBS_UNSAFE=	yes
INSTALL_TARGET=	install-strip
CFLAGS+=	-fcommon

CONFLICTS_INSTALL=	fspclient

SUB_FILES=	pkg-message
WRKSRC=		${WRKDIR}/alliance/src

ALLIANCE_TOP=	${PREFIX}/alliance

post-patch:
	@${REINPLACE_CMD} -e '/include <malloc.h>/d' \
		${WRKSRC}/xgra/src/XSB_parse.c
# Recursive make commands should always use the variable MAKE, not the
# explicit command name `make' (see the GNU make manual, section 5.7.1)
	@${REINPLACE_CMD} -e 's/; make/; $$(MAKE)/' \
		${WRKSRC}/documentation/Makefile.am \
		${WRKSRC}/documentation/alliance-examples/Makefile \
		${WRKSRC}/documentation/tutorials/Makefile.am

pre-configure:
	@cd ${WRKSRC} && ./autostuff

.include <bsd.port.mk>
