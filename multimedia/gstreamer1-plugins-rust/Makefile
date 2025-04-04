PORTNAME=	gstreamer1-plugins-rust
DISTVERSION=	0.7.2
PORTREVISION=	3
CATEGORIES=	multimedia

MAINTAINER=	jbeich@FreeBSD.org
COMMENT=	Various GStreamer plugins written in Rust

LICENSE=	LGPL21+ MIT
LICENSE_COMB=	multi
LICENSE_FILE_MIT=	${WRKSRC}/LICENSE-MIT
LICENSE_FILE_LGPL21+ =	${WRKSRC}/LICENSE-LGPLv2

BUILD_DEPENDS=	cargo-cbuild:devel/cargo-c

USES=		cargo gnome meson pkgconfig ssl
USE_GITLAB=	yes
USE_GNOME=	glib20
USE_GSTREAMER1=	yes
GL_SITE=	https://gitlab.freedesktop.org
GL_ACCOUNT=	gstreamer
GL_PROJECT=	gst-plugins-rs
GL_COMMIT=	d0466b3eee114207f851b37cae0015c0e718f021
MAKE_ENV=	${CARGO_ENV}

CARGO_CRATES=	adler-1.0.2 \
		adler32-1.2.0 \
		aho-corasick-0.7.18 \
		ansi_term-0.11.0 \
		ansi_term-0.12.1 \
		anyhow-1.0.43 \
		arbitrary-0.4.7 \
		arg_enum_proc_macro-0.3.1 \
		array-init-2.0.0 \
		arrayvec-0.5.2 \
		async-compression-0.3.8 \
		async-trait-0.1.51 \
		async-tungstenite-0.14.0 \
		atk-0.14.0 \
		atk-sys-0.14.0 \
		atomic_refcell-0.1.7 \
		atty-0.2.14 \
		autocfg-1.0.1 \
		base-x-0.2.8 \
		base64-0.13.0 \
		bincode-1.3.3 \
		bindgen-0.58.1 \
		bitflags-1.3.2 \
		bitstream-io-1.2.0 \
		bitvec-0.19.5 \
		block-buffer-0.9.0 \
		bumpalo-3.7.0 \
		byte-slice-cast-1.0.0 \
		bytemuck-1.7.2 \
		byteorder-1.4.3 \
		bytes-0.5.6 \
		bytes-1.1.0 \
		cairo-rs-0.14.3 \
		cairo-sys-rs-0.14.0 \
		cc-1.0.69 \
		cdg-0.1.0 \
		cdg_renderer-0.6.0 \
		cexpr-0.4.0 \
		cfg-expr-0.7.4 \
		cfg-if-0.1.10 \
		cfg-if-1.0.0 \
		chrono-0.4.19 \
		clang-sys-1.2.1 \
		clap-2.33.3 \
		claxon-0.4.3 \
		color_quant-1.1.0 \
		const_fn-0.4.8 \
		cookie-0.14.4 \
		cookie_store-0.12.0 \
		core-foundation-0.9.1 \
		core-foundation-sys-0.8.2 \
		cpufeatures-0.2.1 \
		crc-2.0.0 \
		crc-catalog-1.1.1 \
		crc32fast-1.2.1 \
		crossbeam-channel-0.5.1 \
		crossbeam-deque-0.8.1 \
		crossbeam-epoch-0.9.5 \
		crossbeam-utils-0.8.5 \
		crypto-mac-0.11.1 \
		csound-0.1.8 \
		csound-sys-0.1.2 \
		ctor-0.1.20 \
		dasp_frame-0.11.0 \
		dasp_sample-0.11.0 \
		dav1d-0.6.0 \
		dav1d-sys-0.3.4 \
		deflate-0.9.1 \
		diff-0.1.12 \
		digest-0.9.0 \
		dirs-next-2.0.0 \
		dirs-sys-next-0.1.2 \
		discard-1.0.4 \
		ebur128-0.1.6 \
		ed25519-1.2.0 \
		either-1.6.1 \
		encoding_rs-0.8.28 \
		env_logger-0.8.4 \
		field-offset-0.3.4 \
		flate2-1.0.20 \
		fnv-1.0.7 \
		foreign-types-0.3.2 \
		foreign-types-shared-0.1.1 \
		form_urlencoded-1.0.1 \
		fst-0.4.7 \
		fuchsia-zircon-0.3.3 \
		fuchsia-zircon-sys-0.3.3 \
		funty-1.1.0 \
		futures-0.3.16 \
		futures-channel-0.3.16 \
		futures-core-0.3.16 \
		futures-executor-0.3.16 \
		futures-io-0.3.16 \
		futures-macro-0.3.16 \
		futures-sink-0.3.16 \
		futures-task-0.3.16 \
		futures-util-0.3.16 \
		gdk-0.14.0 \
		gdk-pixbuf-0.14.0 \
		gdk-pixbuf-sys-0.14.0 \
		gdk-sys-0.14.0 \
		generic-array-0.14.4 \
		getrandom-0.2.3 \
		gif-0.11.2 \
		gio-0.14.3 \
		gio-sys-0.14.0 \
		glib-0.14.4 \
		glib-macros-0.14.1 \
		glib-sys-0.14.0 \
		glob-0.3.0 \
		gobject-sys-0.14.0 \
		gstreamer-0.17.3 \
		gstreamer-app-0.17.2 \
		gstreamer-app-sys-0.17.0 \
		gstreamer-audio-0.17.2 \
		gstreamer-audio-sys-0.17.0 \
		gstreamer-base-0.17.2 \
		gstreamer-base-sys-0.17.0 \
		gstreamer-check-0.17.0 \
		gstreamer-check-sys-0.17.0 \
		gstreamer-net-0.17.0 \
		gstreamer-net-sys-0.17.0 \
		gstreamer-rtp-0.17.0 \
		gstreamer-rtp-sys-0.17.0 \
		gstreamer-sys-0.17.3 \
		gstreamer-video-0.17.2 \
		gstreamer-video-sys-0.17.0 \
		gtk-0.14.1 \
		gtk-sys-0.14.0 \
		gtk3-macros-0.14.0 \
		h2-0.3.4 \
		hashbrown-0.11.2 \
		headers-0.3.4 \
		headers-core-0.2.0 \
		heck-0.3.3 \
		hermit-abi-0.1.19 \
		hex-0.4.3 \
		hmac-0.11.0 \
		http-0.2.4 \
		http-body-0.4.3 \
		httparse-1.5.1 \
		httpdate-1.0.1 \
		humantime-2.1.0 \
		hyper-0.14.12 \
		hyper-tls-0.5.0 \
		hyphenation-0.8.4 \
		hyphenation_commons-0.8.4 \
		idna-0.2.3 \
		image-0.23.14 \
		indexmap-1.7.0 \
		input_buffer-0.4.0 \
		instant-0.1.10 \
		interpolate_name-0.2.3 \
		iovec-0.1.4 \
		ipnet-2.3.1 \
		itertools-0.10.1 \
		itoa-0.4.8 \
		js-sys-0.3.53 \
		kernel32-sys-0.2.2 \
		lazy_static-1.4.0 \
		lazycell-1.3.0 \
		lewton-0.10.2 \
		lexical-core-0.7.6 \
		libc-0.2.101 \
		libfuzzer-sys-0.3.5 \
		libloading-0.7.0 \
		libsodium-sys-0.2.7 \
		libwebp-sys2-0.1.2 \
		lock_api-0.4.5 \
		log-0.4.14 \
		matches-0.1.9 \
		md-5-0.9.1 \
		memchr-2.4.1 \
		memoffset-0.6.4 \
		mime-0.3.16 \
		minimal-lexical-0.1.2 \
		miniz_oxide-0.4.4 \
		mio-0.6.23 \
		mio-0.7.13 \
		miow-0.2.2 \
		miow-0.3.7 \
		muldiv-1.0.0 \
		native-tls-0.2.8 \
		net2-0.2.37 \
		nnnoiseless-0.3.2 \
		nom-5.1.2 \
		nom-6.1.2 \
		nom-7.0.0 \
		noop_proc_macro-0.3.0 \
		ntapi-0.3.6 \
		num-0.4.0 \
		num-bigint-0.4.1 \
		num-complex-0.3.1 \
		num-complex-0.4.0 \
		num-derive-0.3.3 \
		num-integer-0.1.44 \
		num-iter-0.1.42 \
		num-rational-0.3.2 \
		num-rational-0.4.0 \
		num-traits-0.2.14 \
		num_cpus-1.13.0 \
		once_cell-1.8.0 \
		opaque-debug-0.3.0 \
		openssl-0.10.36 \
		openssl-probe-0.1.4 \
		openssl-sys-0.9.66 \
		output_vt100-0.1.2 \
		pango-0.14.3 \
		pango-sys-0.14.0 \
		pangocairo-0.14.0 \
		pangocairo-sys-0.14.0 \
		parking_lot-0.11.2 \
		parking_lot_core-0.8.5 \
		paste-1.0.5 \
		peeking_take_while-0.1.2 \
		percent-encoding-2.1.0 \
		pest-2.1.3 \
		pin-project-1.0.8 \
		pin-project-internal-1.0.8 \
		pin-project-lite-0.1.12 \
		pin-project-lite-0.2.7 \
		pin-utils-0.1.0 \
		pkg-config-0.3.19 \
		png-0.17.1 \
		pocket-resources-0.3.2 \
		ppv-lite86-0.2.10 \
		pretty-hex-0.2.1 \
		pretty_assertions-0.7.2 \
		primal-check-0.3.1 \
		proc-macro-crate-1.0.0 \
		proc-macro-error-1.0.4 \
		proc-macro-error-attr-1.0.4 \
		proc-macro-hack-0.5.19 \
		proc-macro-nested-0.1.7 \
		proc-macro2-1.0.28 \
		publicsuffix-1.5.6 \
		quote-1.0.9 \
		radium-0.5.3 \
		rand-0.8.4 \
		rand_chacha-0.3.1 \
		rand_core-0.6.3 \
		rand_hc-0.3.1 \
		rav1e-0.4.1 \
		rayon-1.5.1 \
		rayon-core-1.9.1 \
		redox_syscall-0.2.10 \
		redox_users-0.4.0 \
		regex-1.5.4 \
		regex-syntax-0.6.25 \
		remove_dir_all-0.5.3 \
		reqwest-0.11.4 \
		rusoto_core-0.47.0 \
		rusoto_credential-0.47.0 \
		rusoto_s3-0.47.0 \
		rusoto_signature-0.47.0 \
		rust_hawktracer-0.7.0 \
		rust_hawktracer_normal_macro-0.4.1 \
		rust_hawktracer_proc_macro-0.4.1 \
		rustc-hash-1.1.0 \
		rustc_version-0.2.3 \
		rustc_version-0.3.3 \
		rustc_version-0.4.0 \
		rustfft-5.1.1 \
		ryu-1.0.5 \
		same-file-1.0.6 \
		schannel-0.1.19 \
		scopeguard-1.1.0 \
		security-framework-2.4.1 \
		security-framework-sys-2.4.1 \
		semver-0.9.0 \
		semver-0.11.0 \
		semver-1.0.4 \
		semver-parser-0.7.0 \
		semver-parser-0.10.2 \
		serde-1.0.130 \
		serde_bytes-0.11.5 \
		serde_derive-1.0.130 \
		serde_json-1.0.67 \
		serde_urlencoded-0.7.0 \
		sha-1-0.9.8 \
		sha1-0.6.0 \
		sha2-0.9.6 \
		shlex-1.1.0 \
		signal-hook-registry-1.4.0 \
		signature-1.3.1 \
		simd_helpers-0.1.0 \
		slab-0.4.4 \
		smallvec-1.6.1 \
		smawk-0.3.1 \
		socket2-0.4.1 \
		sodiumoxide-0.2.7 \
		standback-0.2.17 \
		static_assertions-1.1.0 \
		stdweb-0.4.20 \
		stdweb-derive-0.5.3 \
		stdweb-internal-macros-0.2.9 \
		stdweb-internal-runtime-0.1.5 \
		strength_reduce-0.2.3 \
		strsim-0.8.0 \
		strum-0.21.0 \
		strum_macros-0.21.1 \
		subtle-2.4.1 \
		syn-1.0.75 \
		system-deps-3.1.2 \
		tap-1.0.1 \
		tempfile-3.2.0 \
		termcolor-1.1.2 \
		textwrap-0.11.0 \
		textwrap-0.14.2 \
		thiserror-1.0.28 \
		thiserror-impl-1.0.28 \
		time-0.1.43 \
		time-0.2.27 \
		time-macros-0.1.1 \
		time-macros-impl-0.1.2 \
		tinyvec-1.3.1 \
		tinyvec_macros-0.1.0 \
		tokio-1.10.1 \
		tokio-macros-1.3.0 \
		tokio-native-tls-0.3.0 \
		tokio-util-0.6.7 \
		toml-0.5.8 \
		tower-service-0.3.1 \
		tracing-0.1.26 \
		tracing-core-0.1.19 \
		transpose-0.2.1 \
		try-lock-0.2.3 \
		tungstenite-0.13.0 \
		typenum-1.13.0 \
		ucd-trie-0.1.3 \
		unicode-bidi-0.3.6 \
		unicode-linebreak-0.1.2 \
		unicode-normalization-0.1.19 \
		unicode-segmentation-1.8.0 \
		unicode-width-0.1.8 \
		unicode-xid-0.2.2 \
		url-2.2.2 \
		utf-8-0.7.6 \
		uuid-0.8.2 \
		v_frame-0.2.2 \
		va_list-0.1.3 \
		vcpkg-0.2.15 \
		vec_map-0.8.2 \
		vergen-3.2.0 \
		version-compare-0.0.11 \
		version_check-0.9.3 \
		walkdir-2.3.2 \
		want-0.3.0 \
		wasi-0.10.2+wasi-snapshot-preview1 \
		wasm-bindgen-0.2.76 \
		wasm-bindgen-backend-0.2.76 \
		wasm-bindgen-futures-0.4.26 \
		wasm-bindgen-macro-0.2.76 \
		wasm-bindgen-macro-support-0.2.76 \
		wasm-bindgen-shared-0.2.76 \
		web-sys-0.3.53 \
		weezl-0.1.5 \
		which-3.1.1 \
		winapi-0.2.8 \
		winapi-0.3.9 \
		winapi-build-0.1.1 \
		winapi-i686-pc-windows-gnu-0.4.0 \
		winapi-util-0.1.5 \
		winapi-x86_64-pc-windows-gnu-0.4.0 \
		winreg-0.7.0 \
		ws2_32-sys-0.2.1 \
		wyz-0.2.0 \
		xml-rs-0.8.4 \
		zeroize-1.4.1 \
		tokio,tokio-macros@git+https://github.com/fengalin/tokio\#2fd1551867c145cabe4548da2e37adc3bdf457a4 \
		flavors@git+https://github.com/rust-av/flavors\#ceb65b8ce94e183c4cf4011da0a40e3a4892c2c0
CARGO_BUILD=	no
CARGO_INSTALL=	no
CARGO_TEST=	no

OPTIONS_DEFINE=	CSOUND DAV1D PANGO SODIUM
OPTIONS_DEFAULT=CSOUND DAV1D PANGO SODIUM
OPTIONS_EXCLUDE_aarch64=	CSOUND # https://github.com/neithanmo/csound-rs/commit/8962b89d7bda
OPTIONS_EXCLUDE_powerpc64le=	CSOUND
OPTIONS_EXCLUDE_powerpc64=	CSOUND
OPTIONS_EXCLUDE_powerpc=	CSOUND DAV1D
OPTIONS_SUB=	yes

CSOUND_DESC=		Audio filtering via Csound
CSOUND_LIB_DEPENDS=	libcsound64.so:audio/csound
CSOUND_CONFIGURE_ENV=	CSOUND_LIB_DIR="${LOCALBASE}/lib"
CSOUND_MESON_ENABLED=	csound

DAV1D_DESC=		AV1 video decoding via libdav1d
DAV1D_BUILD_DEPENDS=	llvm${LLVM_DEFAULT}>0:devel/llvm${LLVM_DEFAULT}
DAV1D_LIB_DEPENDS=	libdav1d.so:multimedia/dav1d
DAV1D_MESON_ENABLED=	dav1d

PANGO_USE=		GNOME=cairo,pango
PANGO_MESON_ENABLED=	closedcaption

SODIUM_DESC=		File encryption and decryption via libsodium
SODIUM_LIB_DEPENDS=	libsodium.so:security/libsodium
SODIUM_MESON_ON=	-Dsodium=system
SODIUM_MESON_OFF=	-Dsodium=disabled

post-patch:
	@${REINPLACE_CMD} -e 's,"llvm-config,&${LLVM_DEFAULT},' \
		${WRKSRC}/cargo-crates/clang-sys-*/build/common.rs \
		${WRKSRC}/cargo-crates/clang-sys-*/src/support.rs
# Make each cargo subcommand very verbose
	@${REINPLACE_CMD} -e "/'cargo'/s/, '--/&verbose'&verbose'&/" \
		${WRKSRC}/cargo_wrapper.py

post-install:
	@${STRIP_CMD} ${STAGEDIR}${PREFIX}/lib/gstreamer-1.0/*.so

.include <bsd.port.mk>
