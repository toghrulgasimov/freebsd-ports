PORTNAME=	qmmp
PORTVERSION=	1.5.3
CATEGORIES=	multimedia
MASTER_SITES=	http://qmmp.ylsoftware.com/files/${PORTNAME}/${PORTVERSION:R}/ \
	SF/qmmp-dev/${PORTNAME}/${PORTVERSION:R}/
PKGNAMESUFFIX=	-qt5

MAINTAINER=	fluffy@FreeBSD.org
COMMENT=	Qt5-based multimedia player

LICENSE=	GPLv2
LICENSE_FILE=	${WRKSRC}/COPYING

CONFLICTS=	${PORTNAME}-0.*
PORTSCOUT=	limit:^1\..*

USES=		cmake gnome pathfix pkgconfig tar:bzip2
USE_QT=		core gui network widgets xml \
		buildtools_build linguisttools_build qmake_build
USE_LDCONFIG=	yes

OPTIONS_SUB=	yes
OPTIONS_GROUP=	DOCUMENTS PLUGIN_APPLICATION PLUGIN_FORMATS \
		PLUGIN_DSP_EFFECTS PLUGIN_VISUAL_EFFECTS PLUGIN_OUTPUT \
		PLUGIN_PLAYLIST PLUGIN_NETWORKING MISC

PLUGIN_APPLICATION_DESC=	Main program view
OPTIONS_GROUP_PLUGIN_APPLICATION=	GNOMEHOTKEY HISTORY HOTKEY KDENOTIFY \
		NOTIFIER QMMP_DIALOG QSUI SKINNEDUI STATICON TWOPANELDIALOG

DOCUMENTS_DESC=	Documentation and API Reference
OPTIONS_GROUP_DOCUMENTS=	DOCS DOXYGEN

PLUGIN_FORMATS_DESC=	Support various media formats
OPTIONS_GROUP_PLUGIN_FORMATS=	ARCHIVE CDDA FAAD FFMPEG FLAC GME \
		MAD MODPLUG MPG123 MUSEPACK OPUS SNDFILE VORBIS WAVPACK WILDMIDI

PLUGIN_DSP_EFFECTS_DESC=	DSP effects
OPTIONS_GROUP_PLUGIN_DSP_EFFECTS=	BS2B CROSSFADE LADSPA SOXR STEREO

PLUGIN_VISUAL_EFFECTS_DESC=	Visual effects
OPTIONS_GROUP_PLUGIN_VISUAL_EFFECTS=	ANALYZER PROJECTM

PLUGIN_OUTPUT_DESC=	Output sound systems
OPTIONS_GROUP_PLUGIN_OUTPUT=	ALSA JACK NULLOUT OSS OSS4 \
		PULSEAUDIO QTMULTIMEDIA SHOUTCAST

PLUGIN_PLAYLIST_DESC=	Playlist operation
OPTIONS_GROUP_PLUGIN_PLAYLIST=	COPYPASTE DIR_ASSOC FILEOPS HAL \
		TRACKCHANGE UDISKS2

PLUGIN_NETWORKING_DESC=	Features via the Net
OPTIONS_GROUP_PLUGIN_NETWORKING=	COVER CURL LYRICS MMS SB SCROBBLER

MISC_DESC=	Other features
OPTIONS_GROUP_MISC=	CONVERTER CUE ENCA FILEWRITER MPLAYER MPRIS RGSCAN SID

OPTIONS_DEFAULT=	ALSA ANALYZER ARCHIVE BS2B CDDA CONVERTER COPYPASTE COVER \
		CROSSFADE CUE CURL DIR_ASSOC ENCA FAAD FFMPEG FILEOPS FILEWRITER FLAC \
		GNOMEHOTKEY GME HAL HISTORY HOTKEY JACK KDENOTIFY LADSPA LYRICS MAD \
		MMS MODPLUG MPG123 MPRIS MPLAYER MUSEPACK NOTIFIER NULLOUT \
		OPUS OSS4 PROJECTM PULSEAUDIO QMMP_DIALOG QSUI QTMULTIMEDIA RGSCAN \
		SHOUTCAST SB SCROBBLER SID SKINNEDUI SNDFILE SOXR STATICON STEREO \
		TRACKCHANGE TWOPANELDIALOG UDISKS2 VORBIS WAVPACK WILDMIDI

DOXYGEN_BUILD_DEPENDS=	doxygen:devel/doxygen

QSUI_DESC=	Simple UI based on standard widgets set
QSUI_CMAKE_BOOL=	USE_QSUI

SKINNEDUI_DESC=	Skinned GUI
SKINNEDUI_USES=	qt:5 xorg
SKINNEDUI_USE=	QT=x11extras XORG=x11
SKINNEDUI_CMAKE_BOOL=	USE_SKINNED

DIR_ASSOC_DESC=	inode/directory mime type association
DIR_ASSOC_CMAKE_BOOL=	USE_DIR_ASSOC
DIR_ASSOC_USES=	desktop-file-utils

JACK_LIB_DEPENDS=	libjack.so:audio/jack \
		libsoxr.so:audio/libsoxr
JACK_BUILD_DEPENDS=	jackit>=0.121.2:audio/jack
JACK_CMAKE_BOOL=	USE_JACK

ALSA_LIB_DEPENDS=	libasound.so:audio/alsa-lib
ALSA_CMAKE_BOOL=	USE_ALSA

BS2B_DESC=		Support the Bauer stereophonic2binaural effect
BS2B_LIB_DEPENDS=	libbs2b.so:audio/libbs2b
BS2B_CMAKE_BOOL=	USE_BS2B

HISTORY_DESC=	Information about listened tracks
HISTORY_USES=	qt:5
HISTORY_USE=	QT=sql
HISTORY_CMAKE_BOOL=	USE_HISTORY

PULSEAUDIO_LIB_DEPENDS=	libpulse.so:audio/pulseaudio
PULSEAUDIO_CMAKE_BOOL=	USE_PULSE

QTMULTIMEDIA_DESC=	Support to use Qt low-level multimedia API
QTMULTIMEDIA_USES=	qt:5
QTMULTIMEDIA_USE=	QT=multimedia
QTMULTIMEDIA_CMAKE_BOOL=	USE_QTMULTIMEDIA

SHOUTCAST_LIB_DEPENDS=	libogg.so:audio/libogg \
		libshout.so:audio/libshout \
		libsoxr.so:audio/libsoxr \
		libvorbis.so:audio/libvorbis
SHOUTCAST_CMAKE_BOOL=	USE_SHOUT

FLAC_LIB_DEPENDS=	libFLAC.so:audio/flac \
		libtag.so:audio/taglib
FLAC_CMAKE_BOOL=	USE_FLAC

MUSEPACK_LIB_DEPENDS=	libmpcdec.so:audio/musepack \
		libtag.so:audio/taglib
MUSEPACK_CMAKE_BOOL=	USE_MPC

GME_DESC=		Support video game music files
GME_LIB_DEPENDS=	libgme.so:audio/libgme
GME_CMAKE_BOOL=	USE_GME

FFMPEG_LIB_DEPENDS=	libavcodec.so:multimedia/ffmpeg
FFMPEG_CMAKE_BOOL=	USE_FFMPEG

MODPLUG_LIB_DEPENDS=	libmodplug.so:audio/libmodplug
MODPLUG_CMAKE_BOOL=	USE_MODPLUG

FAAD_LIB_DEPENDS=	libfaad.so:audio/faad \
		libtag.so:audio/taglib
FAAD_CMAKE_BOOL=	USE_AAC

CDDA_LIB_DEPENDS=	libcdio.so:sysutils/libcdio \
		libcddb.so:audio/libcddb \
		libcdio_cdda.so:sysutils/libcdio-paranoia
CDDA_CMAKE_BOOL=	USE_CDA

ENCA_DESC=		Support automatic character set detection
ENCA_LIB_DEPENDS=	libenca.so:converters/enca
ENCA_CMAKE_BOOL=	USE_ENCA

FILEWRITER_DESC=	Dump output sound into ogg audio file
FILEWRITER_LIB_DEPENDS=	libvorbisenc.so:audio/libvorbis
FILEWRITER_CMAKE_BOOL=	USE_FILEWRITER

MPLAYER_DESC=	Enable showing videos by mplayer
MPLAYER_RUN_DEPENDS=	mplayer:multimedia/mplayer
MPLAYER_CMAKE_BOOL=	USE_MPLAYER

PROJECTM_DESC=	Support the projectM music visualiser
PROJECTM_LIB_DEPENDS=	libprojectM.so:graphics/libprojectm
PROJECTM_USES=		gl
PROJECTM_USE=		GL=gl
PROJECTM_CMAKE_BOOL=	USE_PROJECTM

OSS_CMAKE_BOOL=	USE_OSS

OSS4_DESC=		Open Sound System (ver4) support
OSS4_BUILD_DEPENDS=	${LOCALBASE}/lib/oss/include/sys/soundcard.h:audio/oss
OSS4_CMAKE_BOOL=	USE_OSS4

LADSPA_RUN_DEPENDS=	analyseplugin:audio/ladspa
LADSPA_CMAKE_BOOL=	USE_LADSPA

WILDMIDI_DESC=	Support to playback MIDI files
WILDMIDI_LIB_DEPENDS=	libWildMidi.so:audio/wildmidi
WILDMIDI_CMAKE_BOOL=	USE_MIDI

MAD_LIB_DEPENDS=	libmad.so:audio/libmad \
		libtag.so:audio/taglib
MAD_CMAKE_BOOL=	USE_MAD

MPG123_LIB_DEPENDS=	libmpg123.so:audio/mpg123 \
		libtag.so:audio/taglib
MPG123_CMAKE_BOOL=	USE_MPG123

OPUS_DESC=		Enable reading opusfile tags
OPUS_LIB_DEPENDS=	libopusfile.so:audio/opusfile \
		libopus.so:audio/opus \
		libtag.so:audio/taglib
OPUS_CMAKE_BOOL=	USE_OPUS

RGSCAN_DESC=	ReplayGain scanner
RGSCAN_LIB_DEPENDS=	libtag.so:audio/taglib
RGSCAN_CMAKE_BOOL=	USE_RGSCAN

SNDFILE_LIB_DEPENDS=	libsndfile.so:audio/libsndfile
SNDFILE_CMAKE_BOOL=	USE_SNDFILE

VORBIS_LIB_DEPENDS=	libvorbis.so:audio/libvorbis \
		libogg.so:audio/libogg \
		libtag.so:audio/taglib
VORBIS_CMAKE_BOOL=	USE_VORBIS

WAVPACK_LIB_DEPENDS=	libwavpack.so:audio/wavpack
WAVPACK_CMAKE_BOOL=	USE_WAVPACK

CURL_LIB_DEPENDS=	libcurl.so:ftp/curl
CURL_CMAKE_BOOL=	USE_CURL

MMS_LIB_DEPENDS=	libmms.so:net/libmms
MMS_CMAKE_BOOL=	USE_MMS

CUE_CMAKE_BOOL=	USE_CUE

NULLOUT_DESC=	Support null output
NULLOUT_CMAKE_BOOL=	USE_NULL

SOXR_LIB_DEPENDS=	libsoxr.so:audio/libsoxr
SOXR_CMAKE_BOOL=	USE_SOXR

CROSSFADE_DESC=	Support cross-fade effect
CROSSFADE_CMAKE_BOOL=	USE_CROSSFADE

STEREO_DESC=	Support stereo effect
STEREO_CMAKE_BOOL=	USE_STEREO

ANALYZER_DESC=	Support spectrum analyzer visualization
ANALYZER_CMAKE_BOOL=	USE_ANALYZER

ARCHIVE_DESC=	Read archived media file
ARCHIVE_USES=	libarchive
ARCHIVE_CMAKE_BOOL=	USE_ARCHIVE

CONVERTER_DESC=	Support file type converter
CONVERTER_LIB_DEPENDS=	libtag.so:audio/taglib
CONVERTER_CMAKE_BOOL=	USE_CONVERTER

COPYPASTE_DESC=	Enable copy/paste track infos between playlists
COPYPASTE_CMAKE_BOOL=	USE_COPYPASTE

MPRIS_DESC=	Support the Media Player Remote
MPRIS_USES=	qt:5
MPRIS_USE=	QT=dbus
MPRIS_CMAKE_BOOL=	USE_MPRIS

SCROBBLER_DESC=	Support Libre.fm/Last.fm scrobbler feature
SCROBBLER_CMAKE_BOOL=	USE_SCROBBLER

SID_DESC=	Support sid
SID_LIB_DEPENDS=	libsidplayfp.so:audio/libsidplayfp
SID_CMAKE_BOOL=	USE_SID

STATICON_DESC=	Support to show status icon
STATICON_CMAKE_BOOL=	USE_STATICON

SB_DESC=	Browser for IceCast stream directory
SB_CMAKE_BOOL=	USE_SB

NOTIFIER_DESC=	Support to popup notifier
NOTIFIER_CMAKE_BOOL=	USE_NOTIFIER

LYRICS_DESC=	Support to show lyrics using lyrics.wikia.com
LYRICS_CMAKE_BOOL=	USE_LYRICS

HAL_USES=	qt:5
HAL_USE=	QT=dbus
HAL_CMAKE_BOOL=	USE_HAL

HOTKEY_DESC=	Support global shortcut keys
HOTKEY_USES=	qt:5
HOTKEY_USE=	QT=x11extras XORG=x11
HOTKEY_CMAKE_BOOL=	USE_HOTKEY

GNOMEHOTKEY_DESC=	Support GNOME/Cinnamon shortcut keys
GNOMEHOTKEY_USES=	qt:5
GNOMEHOTKEY_USE=	QT=dbus
GNOMEHOTKEY_CMAKE_BOOL=	USE_GNOMEHOTKEY

FILEOPS_DESC=	Support file operation
FILEOPS_CMAKE_BOOL=	USE_FILEOPS

COVER_DESC=	Support to show cover images
COVER_CMAKE_BOOL=	USE_COVER

KDENOTIFY_DESC=	Support to popup notifier for KDE
KDENOTIFY_USES=	qt:5
KDENOTIFY_USE=	QT=dbus
KDENOTIFY_CMAKE_BOOL=	USE_KDENOTIFY

TRACKCHANGE_DESC=	Enable to run external command each track
TRACKCHANGE_CMAKE_BOOL=	USE_TRACKCHANGE

UDISKS2_DESC=	Support removable disc detection using UDisks
UDISKS2_RUN_DEPENDS=	bsdisks:sysutils/bsdisks
UDISKS2_USES=	qt:5
UDISKS2_USE=	QT=dbus
UDISKS2_CMAKE_BOOL=	USE_UDISKS2

QMMP_DIALOG_DESC=	An original dialog
QMMP_DIALOG_CMAKE_BOOL=	USE_QMMP_DIALOG

TWOPANELDIALOG_DESC=	File dialog by two-panel selector
TWOPANELDIALOG_CMAKE_BOOL=	USE_TWO_PANEL_DIALOG

PLIST_SUB+=	SHLIB_VER=${PORTVERSION:C/-.*//} LIB_SUFFX=-${PORTVERSION:R}

PATHFIX_CMAKELISTSTXT=	\\"CMakeLists.txt -exec grep -l /pkgconfig {} +\\"
PORTDOCS=	README README.RUS AUTHORS

.include <bsd.port.options.mk>

.if (${PORT_OPTIONS:MMAD} || ${PORT_OPTIONS:MMPG123})
PLIST_SUB+=	MPEG=""
.else
PLIST_SUB+=	MPEG="@comment "
.endif

post-patch:
	@${GREP} -L '${LOCALBASE}/lib/oss' \
		${WRKSRC}/src/plugins/Output/oss4/CMakeLists.txt | ${XARGS} \
		${REINPLACE_CMD} -e 's|/usr/local/|${LOCALBASE}/|'

pre-configure:
	@${RM} ${BUILD_WRKSRC}/CMakeCache.txt

post-build-DOXYGEN-on:
	cd ${WRKSRC}/doc && doxygen Doxyfile

post-install-DOCS-on:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}; \
		cd ${WRKSRC} && ${INSTALL_MAN} ${PORTDOCS} ${STAGEDIR}${DOCSDIR}

post-install-DOXYGEN-on:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}/html/search ; \
	cd ${WRKSRC}/doc/html && \
		${INSTALL_MAN} *.html *.png *.css ${STAGEDIR}${DOCSDIR}/html ; \
	cd ${WRKSRC}/doc/html/search && \
		${INSTALL_MAN} *.html *.png *.css *.js ${STAGEDIR}${DOCSDIR}/html/search ; \
	${RM} ${WRKDIR}/PLIST.doc ; \
	${FIND} ${STAGEDIR}${DOCSDIR}/html -type f | \
		${SED} 's|${STAGEDIR}${PREFIX}/||' \
		>> ${WRKDIR}/PLIST.doc ; \
	cd ${WRKDIR} ; ${SED} -i -e '/PLIST.doc/ r PLIST.doc' ${TMPPLIST}

.include <bsd.port.mk>
