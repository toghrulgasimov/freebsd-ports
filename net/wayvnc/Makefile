PORTNAME=	wayvnc
DISTVERSIONPREFIX=	v
DISTVERSION=	0.4.1
CATEGORIES=	net

MAINTAINER=	jbeich@FreeBSD.org
COMMENT=	VNC server for wlroots-based compositors

LICENSE=	ISCL
LICENSE_FILE=	${WRKSRC}/COPYING

BUILD_DEPENDS=	evdev-proto>0:devel/evdev-proto
LIB_DEPENDS=	libaml.so:devel/aml \
		libdrm.so:graphics/libdrm \
		libwayland-client.so:graphics/wayland \
		libneatvnc.so:net/neatvnc \
		libxkbcommon.so:x11/libxkbcommon

USES=		compiler:c11 meson pkgconfig xorg
USE_GITHUB=	yes
USE_XORG=	pixman
USE_LDCONFIG=	yes
GH_ACCOUNT=	any1
PLIST_FILES=	bin/${PORTNAME}

OPTIONS_DEFINE=	MANPAGES OPENGL
OPTIONS_DEFAULT=MANPAGES

MANPAGES_BUILD_DEPENDS=	scdoc:textproc/scdoc
MANPAGES_MESON_ENABLED=	man-pages
MANPAGES_PLIST_FILES=	man/man1/${PORTNAME}.1.gz

OPENGL_USES=		gl
OPENGL_USE=		GL=gbm
OPENGL_MESON_ENABLED=	screencopy-dmabuf

post-patch:
# Extract (snapshot) version from the port instead of meson.build
	@${REINPLACE_CMD} -i .nogit -e 's/git.found()/false/' \
		-e '/project_version/s/@0@/${DISTVERSIONFULL}/' \
		${WRKSRC}/meson.build

.include <bsd.port.mk>
