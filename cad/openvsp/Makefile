PORTNAME=	openvsp
DISTVERSIONPREFIX=	${GH_PROJECT}_
DISTVERSION=	3.26.1
CATEGORIES=	cad

MAINTAINER=	fernape@FreeBSD.org
COMMENT=	Create a 3D model of an aircraft defined by engineering parameters

LICENSE=	NOSA13
LICENSE_NAME=	NASA Open Source Agreement version 1.3
LICENSE_FILE=	${WRKSRC}/LICENSE
LICENSE_PERMS=	dist-mirror dist-sell pkg-mirror pkg-sell auto-accept

BROKEN_aarch64=		fails to compile: invokes x86 asm

BUILD_DEPENDS=	${LOCALBASE}/lib/libopenNURBS.a:graphics/opennurbs \
		${LOCALBASE}/include/glm/glm.hpp:math/glm \
		${LOCALBASE}/libdata/pkgconfig/pthread-stubs.pc:devel/libpthread-stubs
LIB_DEPENDS=	libdrm.so:graphics/libdrm \
		libpng.so:graphics/png \
		libfreetype.so:print/freetype2 \
		libexpat.so:textproc/expat2 \
		libfontconfig.so:x11-fonts/fontconfig \
		libfltk.so:x11-toolkits/fltk \
		libcpptest.so:devel/cpptest

USES=		compiler:c++11-lang cmake:noninja localbase\
		gl gnome jpeg xorg
USE_GITHUB=	yes
GH_ACCOUNT=	${GH_PROJECT}
GH_PROJECT=	OpenVSP

USE_GL=		gl glew glu
USE_GNOME=	libxml2
USE_XORG=	ice sm x11 xau xcb xdamage xdmcp xext xfixes xft \
		xinerama xrender xxf86vm

CXXFLAGS_powerpc64=	-mvsx
CMAKE_ARGS=	-DVSP_USE_SYSTEM_CMINPACK:BOOLEAN=yes \
		-DVSP_USE_SYSTEM_CPPTEST:BOOLEAN=yes \
		-DVSP_USE_SYSTEM_CODEELI:BOOLEAN=no \
		-DVSP_USE_SYSTEM_EIGEN:BOOLEAN=no \
		-DVSP_USE_SYSTEM_LIBXML2:BOOLEAN=yes \
		-DVSP_USE_SYSTEM_FLTK:boolean=yes \
		-DVSP_USE_SYSTEM_CMINPACK:boolean=no \
		-DVSP_USE_SYSTEM_GLM:BOOLEAN=yes \
		-DVSP_USE_SYSTEM_GLEW:BOOLEAN=yes
CMAKE_INSTALL_PREFIX=	${STAGEDIR}${PREFIX}
CMAKE_SOURCE_PATH=	${WRKSRC}/SuperProject

BUILD_PREFIX=	OpenVSP-prefix/src/OpenVSP-build/_CPack_Packages/FreeBSD/ZIP/OpenVSP-${DISTVERSION}-FreeBSD

do-install:
	@${MKDIR} ${STAGEDIR}${DATADIR}
	${INSTALL_DATA} ${BUILD_WRKSRC}/${BUILD_PREFIX}/vspIcon.png ${STAGEDIR}${DATADIR}
	${RM} ${STAGEDIR}${PREFIX}/vspIcon.png ${BUILD_WRKSRC}/${BUILD_PREFIX}/vspIcon.png
.for f in vsp vspaero vspscript vspslicer vspviewer
	${INSTALL_PROGRAM} ${BUILD_WRKSRC}/${BUILD_PREFIX}/${f} ${STAGEDIR}${PREFIX}/bin
	${RM} ${STAGEDIR}${PREFIX}/${f}
.endfor
.for d in CustomScripts airfoil matlab scripts textures
	(cd ${BUILD_WRKSRC}/${BUILD_PREFIX}/${d} && ${COPYTREE_SHARE} . ${STAGEDIR}${DATADIR})
	${RM} -rf ${STAGEDIR}${PREFIX}/${d}
.endfor
	${CP} ${BUILD_WRKSRC}/${BUILD_PREFIX}/LICENSE ${STAGEDIR}${DATADIR}
	${RM} ${STAGEDIR}${PREFIX}/LICENSE

.include <bsd.port.mk>
