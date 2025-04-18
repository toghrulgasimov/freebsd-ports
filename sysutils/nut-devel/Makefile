# Created by: Boris Popov <bp@FreeBSD.org>

PORTNAME=	nut
PORTVERSION=	${NUT_COMMIT_DATE}
CATEGORIES=	sysutils
PKGNAMESUFFIX=	-devel
# MASTER_SITES=	http://www.networkupstools.org/source/${PORTVERSION:R}/
# DISTFILES=	${DISTNAME}${EXTRACT_SUFX}
# EXTRACT_ONLY=	${DISTNAME}${EXTRACT_SUFX}

MAINTAINER=	cy@FreeBSD.org
COMMENT=	Network UPS Tools

USE_GITHUB=	yes
GH_ACCOUNT=	networkupstools
GH_TAGNAME=	92ecace7
NUT_COMMIT_DATE=	2021.12.28

MAKE_JOBS_UNSAFE=	yes
GNU_CONFIGURE=	yes
USE_LDCONFIG=	yes
USES=		autoreconf:build compiler:c11 gmake libtool pkgconfig python:build

NUT_USER?=	uucp
NUT_GROUP?=	uucp
STATEDIR?=	/var/db/nut
PLIST_SUB+=	NUT_USER=${NUT_USER}
PLIST_SUB+=	NUT_GROUP=${NUT_GROUP}

OPTIONS_DEFAULT=SERIAL USB SNMP NEON IPMI_OFF SSL_OFF
OPTIONS_DEFINE=	SERIAL USB SNMP NEON PDU CGI BASH AVAHI DOCS
OPTIONS_SINGLE=	IPMI SSL
OPTIONS_SINGLE_IPMI=	IPMI_OFF IPMIPSU FREEIPMI
OPTIONS_SINGLE_SSL=	SSL_OFF OPENSSL NSS

SERIAL_DESC=	SERIAL support
USB_DESC=	USB support
SNMP_DESC=	SNMP support
NEON_DESC=	NEON XML/HTTP support
PDU_DESC=	Powerman PDU support
CGI_DESC=	Web CGI interface
BASH_DESC=	Bash Completion support
AVAHI_DESC=	Avahi support
IPMI_OFF_DESC=	No IPMI support
FREEIPMI_DESC=	freeipmi support
IPMIPSU_DESC=	Use nut-ipmipsu support (experimental)
SSL_OFF_DESC=	No SSL support

USE_RC_SUBR=	nut nut_upsmon nut_upslog
SUB_LIST+=	STATEDIR=${STATEDIR}
PLIST_SUB+=	STATEDIR=${STATEDIR}

PORTDOCS=	*

.include <bsd.port.options.mk>

TMPDIR?=	/tmp
CONFIGURE_ARGS=	--sysconfdir=${PREFIX}/etc/nut \
		--program-transform-name="" \
		--localstatedir=${STATEDIR} \
		--datadir=${PREFIX}/etc/nut \
		--with-devd-dir=${PREFIX}/etc/devd \
		--with-drvpath=${PREFIX}/libexec/nut \
		--with-statepath=${STATEDIR} \
		--with-altpidpath=${STATEDIR} \
		--with-pidpath=${STATEDIR} \
		--with-pkgconfig-dir=${PREFIX}/libdata/pkgconfig \
		--with-user=${NUT_USER} \
		--with-group=${NUT_GROUP} \
		--with-dev

CFLAGS+=	-I${LOCALBASE}/include -L${LOCALBASE}/lib
LIB_DEPENDS+=	libltdl.so:devel/libltdl

BUILD_DEPENDS=	asciidoc:textproc/asciidoc

.if ${PORT_OPTIONS:MCGI}
LIB_DEPENDS+=	libgd.so:graphics/gd
CGIDIR?=	${PREFIX}/www/cgi-bin/${PORTNAME}
CGIDIR_REL?=	${CGIDIR:S,^${PREFIX}/,,}
CONFIGURE_ARGS+=	--with-cgi --with-cgipath=${CGIDIR} \
			--with-htmlpath=${WWWDIR} \
			--with-gd-includes=-I${LOCALBASE}/include \
			--with-gd-libs="-L${LOCALBASE}/lib -lgd"
PLIST_SUB+=	NUT_CGI=""
PLIST_SUB+=	CGIDIR="${CGIDIR_REL}"
PLIST_SUB+=	CGIETCDIR="etc/nut/"
.else
CONFIGURE_ARGS+=	--without-cgi
PLIST_SUB+=	NUT_CGI="@comment "
.endif

.if ${PORT_OPTIONS:MSERIAL}
CONFIGURE_ARGS+=	--with-serial
PLIST_SUB+=	NUT_SERIAL=""
.else
CONFIGURE_ARGS+=	--without-serial
PLIST_SUB+=	NUT_SERIAL="@comment "
.endif

.if ${PORT_OPTIONS:MUSB}
#EXTRA_PATCHES=	${FILESDIR}/extra-patch-m4_nut_check_libusb.m4
CONFIGURE_ARGS+=	--with-usb=auto
PLIST_SUB+=	NUT_USB=""
.else
CONFIGURE_ARGS+=	--without-usb
PLIST_SUB+=	NUT_USB="@comment "
.endif

.if ${PORT_OPTIONS:MSNMP}
LIB_DEPENDS+=	libnetsnmp.so:net-mgmt/net-snmp
CONFIGURE_ARGS+=	--with-snmp
PLIST_SUB+=	NUT_SNMP=""
.else
CONFIGURE_ARGS+=	--without-snmp
PLIST_SUB+=	NUT_SNMP="@comment "
.endif

.if ${PORT_OPTIONS:MNEON}
LIB_DEPENDS+=	libneon.so:www/neon
CONFIGURE_ARGS+=	--with-neon
PLIST_SUB+=	NUT_NEON=""
.else
CONFIGURE_ARGS+=	--without-neon
CONFIGURE_ARGS+=	--disable-neon
PLIST_SUB+=	NUT_NEON="@comment "
.endif

.if ${PORT_OPTIONS:MPDU}
LIB_DEPENDS+=	libpowerman.so:sysutils/powerman
CONFIGURE_ARGS+=	--with-powerman
PLIST_SUB+=	NUT_PDU=""
.else
CONFIGURE_ARGS+=	--without-powerman
PLIST_SUB+=	NUT_PDU="@comment "
.endif

.if ${PORT_OPTIONS:MBASH}
BUILD_DEPENDS+=	${LOCALBASE}/share/bash-completion/bash_completion.sh:shells/bash-completion
RUN_DEPENDS+=	${LOCALBASE}/share/bash-completion/bash_completion.sh:shells/bash-completion
PLIST_SUB+=	BASH=""
.else
PLIST_SUB+=	BASH="@comment "
.endif

.if ${PORT_OPTIONS:MAVAHI}
BUILD_DEPENDS+=	${LOCALBASE}/include/avahi-ui/avahi-ui.h:net/avahi-header
BUILD_DEPENDS+=	avahi-daemon:net/avahi-app
RUN_DEPENDS+=	avahi-daemon:net/avahi-app
CONFIGURE_ARGS+=	--with-avahi
.else
CONFIGURE_ARGS+=	--without-avahi
.endif

.if ${PORT_OPTIONS:MFREEIPMI}
LIB_DEPENDS+=	libfreeipmi.so:sysutils/freeipmi
CONFIGURE_ARGS+=	--with-freeipmi
PLIST_SUB+=	NUT_FREEIPMI=""
.else
CONFIGURE_ARGS+=	--without-freeipmi
PLIST_SUB+=	NUT_FREEIPMI="@comment "
.endif

.if ${PORT_OPTIONS:MIPMIPSU}
LIB_DEPENDS+=	libfreeipmi.so:sysutils/freeipmi
CONFIGURE_ARGS+=	--with-ipmi
PLIST_SUB+=	NUT_IPMIPSU=""
.else
CONFIGURE_ARGS+=	--without-ipmi
PLIST_SUB+=	NUT_IPMIPSU="@comment "
.endif

.if ${PORT_OPTIONS:MOPENSSL}
USES+=	ssl
CONFIGURE_ARGS+=	--with-openssl
.elif ${PORT_OPTIONS:MNSS}
LIB_DEPENDS=		libnss3.so:security/nss
CONFIGURE_ARGS+=	--with-nss
.else
CONFIGURE_ARGS+=	--without-openssl --without-ssl
.endif

post-patch:
	@${REINPLACE_CMD} -i '' -e 's|python|${PYTHON_CMD}|' ${WRKSRC}/autogen.sh
	@${FIND} ${WRKSRC} -type f | ${XARGS} ${REINPLACE_CMD} -i '' -e 's|/usr/bin/env python|${PYTHON_CMD}|'

pre-configure:
	cd ${WRKSRC} && ./autogen.sh

pre-install:
	@${MKDIR} ${STAGEDIR}${PREFIX}/libexec/nut
	@${REINPLACE_CMD} -e 's/device-name\*/cdev/g' ${WRKSRC}/scripts/devd/nut-usb.conf

post-install:
	@${MKDIR} ${STAGEDIR}${STATEDIR}
	@${MKDIR} ${STAGEDIR}${PREFIX}/etc/syslog.d
.if ${PORT_OPTIONS:MBASH}
	@${MKDIR} ${STAGEDIR}${PREFIX}/etc/bash_completion.d/
	${INSTALL_DATA} ${WRKSRC}/scripts/misc/nut.bash_completion ${STAGEDIR}${PREFIX}/etc/bash_completion.d/
.endif
.if ${PORT_OPTIONS:MDOCS}
	@${MKDIR} ${STAGEDIR}${DOCSDIR}/cables
	${INSTALL_DATA} ${WRKSRC}/docs/cables/*.txt ${STAGEDIR}${DOCSDIR}/cables
	${INSTALL_DATA} ${WRKSRC}/docs/*.txt ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/docs/FAQ.txt ${STAGEDIR}${DOCSDIR}
.for file in AUTHORS COPYING INSTALL MAINTAINERS NEWS README UPGRADING
	${INSTALL_DATA} ${WRKSRC}/${file} ${STAGEDIR}${DOCSDIR}
.endfor
.endif
	@${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	${INSTALL_DATA} ${PATCHDIR}/nut.syslog ${STAGEDIR}${EXAMPLESDIR}/syslog.sample
	${INSTALL_DATA} ${PATCHDIR}/nut.newsyslog ${STAGEDIR}${EXAMPLESDIR}/newsyslog.sample
	${MKDIR} ${STAGEDIR}/var/log/nut

.include <bsd.port.mk>
