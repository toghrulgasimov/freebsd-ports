# Created by: Sergey Matveychuk <sem@FreeBSD.org>

PORTNAME=	unbound
DISTVERSION=	1.14.0
CATEGORIES=	dns
MASTER_SITES=	https://www.nlnetlabs.nl/downloads/unbound/ \
		https://distfiles.crux.guru/

MAINTAINER=	jaap@NLnetLabs.nl
COMMENT=	Validating, recursive, and caching DNS resolver

LICENSE=	BSD3CLAUSE
LICENSE_FILE=	${WRKSRC}/LICENSE

LIB_DEPENDS=	libexpat.so:textproc/expat2

USES=		autoreconf cpe libtool pkgconfig ssl

CPE_VENDOR=	nlnetlabs
GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--with-ssl=${OPENSSLBASE} --with-libexpat=${LOCALBASE}
USE_LDCONFIG=	yes
TEST_TARGET=	test

USERS=		${PORTNAME}
GROUPS=		${PORTNAME}

USE_RC_SUBR=	unbound

PORTDOCS=	CREDITS Changelog FEATURES LICENSE README \
		README.DNS64  README.ipset.md README.svn README.tests \
		TODO control_proto_spec.txt ietf67-design-02.odp \
		ietf67-design-02.pdf requirements.txt example.conf \
		CNAME-basedRedirectionDesignNotes.pdf IP-BasedActions.pdf

OPTIONS_SUB=	yes
OPTIONS_DEFINE=	THREADS PYTHON GOST ECDSA MUNIN_PLUGIN DOCS LIBEVENT \
		FILTER_AAAA DNSTAP DNSCRYPT SUBNET EVAPI TFOCL TFOSE \
		HIREDIS DOH DEP-RSA1024
OPTIONS_DEFAULT=THREADS ECDSA LIBEVENT GOST DOH

LIBEVENT_DESC=	Build against libevent
GOST_DESC=	Enable GOST support (requires OpenSSL >= 1.0)
ECDSA_DESC=	Enable ECDSA (elliptic curve) support (OpenSSL >= 1.0)
MUNIN_PLUGIN_DESC=	Install Munin plugin
FILTER_AAAA_DESC=	Build with AAAA filter functionality (contrib)
DNSTAP_DESC=	Enable dnstap logging support
DNSCRYPT_DESC=	Enable dnscrypt support
SUBNET_DESC=	Enable client subnet support
EVAPI_DESC=	(Experimental) pluggable event based libunbound API support
TFOCL_DESC=	Enable TCP Fast Open for client mode
TFOSE_DESC=	Enable TCP Fast Open for server mode
HIREDIS_DESC=	Enable hiredis support for the cachedb module
DOH_DESC=	Enable DNS-over-HTTPS support
DEP-RSA1024_DESC=	Deprecate the use of RSA 1024 keys

STRIP_FILES=	.libs/libunbound.so unbound-checkconf unbound \
		unbound-control .libs/unbound-host .libs/unbound-anchor

DNSTAP_CONFIGURE_ENABLE=dnstap
DNSTAP_LIB_DEPENDS=	libfstrm.so:devel/fstrm \
			libprotobuf-c.so:devel/protobuf-c
DNSCRYPT_CONFIGURE_ENABLE=	dnscrypt
DNSCRYPT_LIB_DEPENDS=	libsodium.so:security/libsodium
SUBNET_CONFIGURE_ENABLE=	subnet
EVAPI_CONFIGURE_ENABLE=	event-api
TFOCL_CONFIGURE_ENABLE=	tfo-client
TFOSE_CONFIGURE_ENABLE=	tfo-server
ECDSA_CONFIGURE_ENABLE=	ecdsa
ECDSA_VARS=		DEPENDS_ARGS+=WITH_ECDSA=yes
GOST_CONFIGURE_ENABLE=	gost
GOST_VARS=		DEPENDS_ARGS+=WITH_GOST=yes
LIBEVENT_CONFIGURE_WITH=libevent
LIBEVENT_CPPFLAGS+=	$$(pkg-config libevent --cflags-only-I)
LIBEVENT_LIB_DEPENDS=	libevent.so:devel/libevent
LIBEVENT_LDFLAGS+=	$$(pkg-config libevent --libs-only-L)
MUNIN_PLUGIN_SUB_FILES=	pkg-message
PYTHON_BUILD_DEPENDS=	swig:devel/swig
PYTHON_CONFIGURE_ON=	--with-pyunbound=yes --with-pythonmodule=yes \
			LDFLAGS="-L${LOCALBASE}/lib" \
			ac_cv_path_SWIG=${LOCALBASE}/bin/swig
PYTHON_USES=		python
PYTHON_VARS=		STRIP_FILES+=.libs/_unbound.so
THREADS_CONFIGURE_WITH=	pthreads
HIREDIS_CONFIGURE_ON=	--enable-cachedb --with-libhiredis
HIREDIS_LIB_DEPENDS=	libhiredis.so:databases/hiredis
DOH_CONFIGURE_ON=	--with-libnghttp2
DOH_LIB_DEPENDS=	libnghttp2.so:www/libnghttp2
DEP-RSA1024_CONFIGURE_ON=	--with-deprecate-rsa-1024

post-patch:
	@${RM} ${WRKSRC}/util/configlexer.c
	@${REINPLACE_CMD} -e 's|if test ! -e $$(DESTDIR)$$(configfile); then || ; \
		s|$$(configfile); fi|$$(configfile).sample|' \
		${WRKSRC}/Makefile.in

post-patch-FILTER_AAAA-on:
	 ${CAT} ${WRKSRC}/contrib/aaaa-filter-iterator.patch | ${PATCH} -d ${WRKSRC} -p1 -s

post-build:
	@for s in ${STRIP_FILES}; do ${STRIP_CMD} ${WRKSRC}/$$s; done

post-install-PYTHON-on:
	@${STRIP_CMD} ${STAGEDIR}${PYTHON_SITELIBDIR}/_unbound.so

post-install-MUNIN_PLUGIN-on:
	@${MKDIR} ${STAGEDIR}${PREFIX}/share/munin/plugins
	${INSTALL_SCRIPT} ${WRKDIR}/unbound-${DISTVERSION}/contrib/unbound_munin_ \
		${STAGEDIR}${PREFIX}/share/munin/plugins/
	@${ECHO_MSG}
	@${ECHO_MSG} "============================================================="
	@${CAT} ${WRKDIR}/pkg-message
	@${ECHO_MSG} "============================================================="

post-install-DOCS-on:
	${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${PORTDOCS:S|^|${WRKSRC}/doc/|} ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
