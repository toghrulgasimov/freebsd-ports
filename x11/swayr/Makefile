PORTNAME=	swayr
DISTVERSIONPREFIX=	v
DISTVERSION=	0.11.2
CATEGORIES=	x11
MASTER_SITES=	https://git.sr.ht/~tsdh/${PORTNAME}/archive/${DISTVERSIONFULL}${EXTRACT_SUFX}?dummy=/
# XXX Teach USES=cargo to not override default DISTFILES
DISTFILES=	${DISTNAME}${EXTRACT_SUFX}

MAINTAINER=	jbeich@FreeBSD.org
COMMENT=	Urgent-first/LRU window switcher for sway

LICENSE=	GPLv3+
LICENSE_FILE=	${WRKSRC}/LICENSE

USES=		cargo
PLIST_FILES=	bin/${PORTNAME} \
		bin/${PORTNAME}d

CARGO_CRATES=	aho-corasick-0.7.18 \
		atty-0.2.14 \
		autocfg-1.0.1 \
		bitflags-1.3.2 \
		cfg-if-1.0.0 \
		clap-3.0.0-rc.5 \
		clap_derive-3.0.0-rc.5 \
		directories-4.0.1 \
		dirs-sys-0.3.6 \
		getrandom-0.2.3 \
		hashbrown-0.11.2 \
		heck-0.3.3 \
		hermit-abi-0.1.19 \
		indexmap-1.7.0 \
		itoa-1.0.1 \
		lazy_static-1.4.0 \
		libc-0.2.112 \
		memchr-2.4.1 \
		os_str_bytes-6.0.0 \
		ppv-lite86-0.2.15 \
		proc-macro-error-1.0.4 \
		proc-macro-error-attr-1.0.4 \
		proc-macro2-1.0.34 \
		quote-1.0.10 \
		rand-0.8.4 \
		rand_chacha-0.3.1 \
		rand_core-0.6.3 \
		rand_hc-0.3.1 \
		redox_syscall-0.2.10 \
		redox_users-0.4.0 \
		regex-1.5.4 \
		regex-syntax-0.6.25 \
		ryu-1.0.9 \
		serde-1.0.131 \
		serde_derive-1.0.131 \
		serde_json-1.0.73 \
		strsim-0.10.0 \
		swayipc-3.0.0-alpha.3 \
		swayipc-types-1.0.0-alpha.3 \
		syn-1.0.82 \
		termcolor-1.1.2 \
		textwrap-0.14.2 \
		thiserror-1.0.30 \
		thiserror-impl-1.0.30 \
		toml-0.5.8 \
		unicode-segmentation-1.8.0 \
		unicode-xid-0.2.2 \
		version_check-0.9.3 \
		wasi-0.10.2+wasi-snapshot-preview1 \
		winapi-0.3.9 \
		winapi-i686-pc-windows-gnu-0.4.0 \
		winapi-util-0.1.5 \
		winapi-x86_64-pc-windows-gnu-0.4.0

post-patch:
# Respect PREFIX for config and icons
	@${REINPLACE_CMD} -e 's,/usr/share,${DATADIR:H},' \
		-e 's,/etc,${PREFIX}&,' \
		${WRKSRC}/src/config.rs \
		${WRKSRC}/src/util.rs

.include <bsd.port.mk>
