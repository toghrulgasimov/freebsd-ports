# Created by: Arun Sharma <arun@sharma-home.net>

PORTNAME=	tbb
PORTVERSION=	2020.3
DISTVERSIONPREFIX=	v
PORTREVISION=	4
CATEGORIES=	devel

MAINTAINER=	martymac@FreeBSD.org
COMMENT=	Library that provides thread building blocks (legacy version)

LICENSE=	APACHE20

ONLY_FOR_ARCHS=		aarch64 amd64 armv6 armv7 i386 powerpc powerpc64 powerpc64le powerpcspe
ONLY_FOR_ARCHS_REASON=	has not been ported to this platform

USES=	compiler gmake tar:tgz

CONFLICTS=	onetbb

USE_GITHUB=	yes
GH_ACCOUNT=	oneapi-src
GH_PROJECT=	oneTBB

SUB_FILES=	tbb.pc
SUB_LIST=	prefix="${PREFIX}" \
		name="${PORTNAME}" \
		description="${COMMENT}" \
		version="${PORTVERSION}"

PLIST=	${WRKDIR}/.PLIST.more

OPTIONS_DEFINE=	DOCS
DOCS_BUILD_DEPENDS=	doxygen:devel/doxygen \
		dot:graphics/graphviz

USE_LDCONFIG=	yes
ALL_TARGET=	default

CC_BASENAME=	${CC:C,^.*/,,}

.include <bsd.port.pre.mk>

post-extract:
.if ${CC_BASENAME} != ${COMPILER_TYPE}
	@${LN} -sf FreeBSD.${COMPILER_TYPE}.inc ${WRKSRC}/build/FreeBSD.${CC_BASENAME}.inc
.endif
	@${CP} ${FILESDIR}/version_info_FreeBSD.sh ${WRKSRC}/build/

post-patch:
	@${REINPLACE_CMD} \
		-e '/^CONLY =/s|^CONLY =.*|CONLY = ${CC}|' \
		-e '/^CPLUS =/s|^CPLUS =.*|CPLUS = ${CXX}|' \
			${WRKSRC}/build/FreeBSD.${COMPILER_TYPE}.inc

post-build-DOCS-on:
	cd ${WRKSRC}; \
		${MAKE_CMD} doxygen

pre-install:
	@${CAT} ${PKGDIR}/pkg-plist >${PLIST}
.if ${PORT_OPTIONS:MDOCS}
	cd ${WRKSRC}/html && \
		${FIND} . -type f | \
		${SED} 's|^\.|%%PORTDOCS%%%%DOCSDIR%%|' >>${PLIST}
.endif

do-install:
	cd ${WRKSRC}; \
	${INSTALL_LIB} build/FreeBSD*release/libtbb.so \
		${STAGEDIR}${PREFIX}/lib/libtbb.so.2; \
	${LN} -sf libtbb.so.2 \
		${STAGEDIR}${PREFIX}/lib/libtbb.so; \
	${INSTALL_LIB} build/FreeBSD*release/libtbbmalloc.so \
		${STAGEDIR}${PREFIX}/lib/libtbbmalloc.so.2; \
	${LN} -sf libtbbmalloc.so.2 \
		${STAGEDIR}${PREFIX}/lib/libtbbmalloc.so; \
	${MKDIR} ${STAGEDIR}${PREFIX}/include/tbb/; \
	cd include/tbb/ && \
		${COPYTREE_SHARE} \
			. ${STAGEDIR}${PREFIX}/include/tbb/ "! -name *\.html"

post-install:
	${INSTALL_DATA} ${WRKDIR}/tbb.pc ${STAGEDIR}${PREFIX}/libdata/pkgconfig

post-install-DOCS-on:
	${MKDIR} ${STAGEDIR}${DOCSDIR}
	cd ${WRKSRC}/html && \
		${COPYTREE_SHARE} . ${STAGEDIR}${DOCSDIR}

.include <bsd.port.post.mk>
