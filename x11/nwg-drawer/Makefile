PORTNAME=	nwg-drawer
DISTVERSIONPREFIX=	v
DISTVERSION=	0.2.3
CATEGORIES=	x11

MAINTAINER=	jbeich@FreeBSD.org
COMMENT=	Application drawer for sway and other wlroots compositors

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE

LIB_DEPENDS=	libfontconfig.so:x11-fonts/fontconfig \
		libgtk-layer-shell.so:x11-toolkits/gtk-layer-shell
RUN_DEPENDS=	xdg-open:devel/xdg-utils

USES=		gnome go:modules pkgconfig
USE_GITHUB=	yes
USE_GNOME=	cairo gdkpixbuf2 gtk30
GH_ACCOUNT=	nwg-piotr
GH_TUPLE=	allan-simon:go-singleinstance:d0997106ab37:allan_simon_go_singleinstance/vendor/github.com/allan-simon/go-singleinstance \
		dlasky:gotk3-layershell:e6ecab2731f7:dlasky_gotk3_layershell/vendor/github.com/dlasky/gotk3-layershell \
		fsnotify:fsnotify:v1.5.1:fsnotify_fsnotify/vendor/github.com/fsnotify/fsnotify \
		golang:sync:56d357773e84:golang_sync/vendor/golang.org/x/sync \
		golang:sys:0f9fa26af87c:golang_sys/vendor/golang.org/x/sys \
		gotk3:gotk3:v0.6.1:gotk3_gotk3/vendor/github.com/gotk3/gotk3 \
		joshuarubin:go-sway:v0.0.4:joshuarubin_go_sway/vendor/github.com/joshuarubin/go-sway \
		joshuarubin:lifecycle:v1.0.0:joshuarubin_lifecycle/vendor/github.com/joshuarubin/lifecycle \
		sirupsen:logrus:v1.8.1:sirupsen_logrus/vendor/github.com/sirupsen/logrus \
		uber-go:atomic:v1.3.2:uber_go_atomic/vendor/go.uber.org/atomic \
		uber-go:multierr:v1.1.0:uber_go_multierr/vendor/go.uber.org/multierr
CGO_LDFLAGS+=	-Wl,--as-needed # harfbuzz, freetype2
PLIST_FILES=	bin/${PORTNAME}
PORTDATA=	desktop-directories *.css

post-patch:
# Respect PREFIX for *.desktop
	@${REINPLACE_CMD} 's,/usr/share,${DATADIR:H},' \
		${WRKSRC}/tools.go

post-install:
# Based on install from WRKSRC/Makefile
	(cd ${WRKSRC} && ${COPYTREE_SHARE} "${PORTDATA}" \
		${STAGEDIR}${DATADIR})

.include <bsd.port.mk>
