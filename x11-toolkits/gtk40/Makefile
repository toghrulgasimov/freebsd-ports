PORTNAME=	gtk
PORTVERSION=	4.6.0
CATEGORIES=	x11-toolkits
MASTER_SITES=	GNOME
PKGNAMESUFFIX=	4
DIST_SUBDIR=	gnome

MAINTAINER=	desktop@FreeBSD.org
COMMENT=	Gimp Toolkit for X11 GUI (current stable version)

LICENSE=	LGPL20

PORTSCOUT=	limit:1,even

BUILD_DEPENDS=	sassc>0:textproc/sassc
LIB_DEPENDS=	libepoxy.so:graphics/libepoxy \
		libpng.so:graphics/png \
		libtiff.so:graphics/tiff \
		libfribidi.so:converters/fribidi \
		libfontconfig.so:x11-fonts/fontconfig \
		libfreetype.so:print/freetype2 \
		libgraphene-1.0.so:graphics/graphene \
		libharfbuzz.so:print/harfbuzz
RUN_DEPENDS=	hicolor-icon-theme>=0:misc/hicolor-icon-theme \
		adwaita-icon-theme>=0:x11-themes/adwaita-icon-theme

USES=		compiler:c11 cpe gettext gnome jpeg localbase meson \
		ninja pathfix perl5 python:3.7+ pkgconfig tar:xz
CPE_VENDOR=	gnome
USE_LDCONFIG=	yes
USE_PERL5=	build
USE_GNOME=	atk cairo gdkpixbuf2 introspection:build pango \
		librsvg2:run
LDFLAGS+=	-lexecinfo

BINARY_ALIAS=	python3=${PYTHON_CMD}

LIBVERSION=	1.600.0
PLIST_SUB+=	LIBVERSION=${LIBVERSION}

GLIB_SCHEMAS=	org.gtk.Demo4.gschema.xml \
		org.gtk.gtk4.Settings.ColorChooser.gschema.xml \
		org.gtk.gtk4.Settings.Debug.gschema.xml \
		org.gtk.gtk4.Settings.EmojiChooser.gschema.xml \
		org.gtk.gtk4.Settings.FileChooser.gschema.xml

OPTIONS_DEFINE=	CUPS COLORD DEBUG BROADWAY FFMPEG \
		GSTREAMER VULKAN WAYLAND X11
OPTIONS_DEFAULT=CUPS COLORD BROADWAY VULKAN WAYLAND X11
OPTIONS_SUB=	yes

BROADWAY_DESC=	Enable GDK Broadway backend for showing GTK+ in the webbrowser using HTML5 and web sockets.
BROADWAY_MESON_TRUE=	broadway-backend

COLORD_DESC=	Color profile support
COLORD_LIB_DEPENDS=	libcolord.so:graphics/colord
COLORD_MESON_ENABLED=	colord

CUPS_LIB_DEPENDS=	libcups.so:print/cups
CUPS_MESON_ENABLED=	print-cups

FFMPEG_DESC=		FFmpeg multimedia backend
FFMPEG_MESON_ENABLED=	media-ffmpeg
FFMPEG_RUN_DEPENDS=	ffmpeg>0:multimedia/ffmpeg
FFMPEG_LIB_DEPENDS=	libavcodec.so:multimedia/ffmpeg

GSTREAMER_DESC=		GStreamer multimedia backend
GSTREAMER_MESON_ENABLED=media-gstreamer
GSTREAMER_USE=		GSTREAMER1=bad,gl

VULKAN_DESC=		GDK Vulkan renderer backend
VULKAN_BUILD_DEPENDS=	vulkan-headers>0:graphics/vulkan-headers
VULKAN_LIB_DEPENDS=	libvulkan.so:graphics/vulkan-loader
VULKAN_RUN_DEPENDS=	vulkan-headers>0:graphics/vulkan-headers
VULKAN_MESON_ENABLED=	vulkan

WAYLAND_DESC=		GDK Wayland backend
WAYLAND_MESON_TRUE=	wayland-backend
WAYLAND_BUILD_DEPENDS=	wayland-protocols>=0:graphics/wayland-protocols
WAYLAND_LIB_DEPENDS=	libwayland-egl.so:graphics/wayland \
			libxkbcommon.so:x11/libxkbcommon
WAYLAND_RUN_DEPENDS=	gsettings-desktop-schemas>=0:devel/gsettings-desktop-schemas \
			wayland-protocols>=0:graphics/wayland-protocols
WAYLAND_USES=		gl
WAYLAND_USE=		GL=egl

X11_DESC=		GDK X11 backend
X11_MESON_TRUE=		x11-backend
X11_USES=		xorg
X11_USE=		XORG=x11,xcomposite,xcursor,xdamage,xext,xfixes,xi,xinerama,xrandr,xrender

pre-build:
	@${RM} -r ${WRKSRC}/docs/gtk.info*

post-install:
	@${MKDIR} ${STAGEDIR}${PREFIX}/lib/gtk-4.0/engines
	@${MKDIR} ${STAGEDIR}${PREFIX}/lib/gtk-4.0/loaders
	@${MKDIR} ${STAGEDIR}${PREFIX}/lib/gtk-4.0/modules
	@${MKDIR} ${STAGEDIR}${PREFIX}/lib/gtk-4.0/${GTK4_VERSION}/engines
	@${MKDIR} ${STAGEDIR}${PREFIX}/lib/gtk-4.0/${GTK4_VERSION}/loaders
	@${MKDIR} ${STAGEDIR}${PREFIX}/lib/gtk-4.0/${GTK4_VERSION}/modules

.include <bsd.port.mk>
