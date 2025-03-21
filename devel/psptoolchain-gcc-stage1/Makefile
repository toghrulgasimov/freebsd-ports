# Created by: Tassilo Philipp <tphilipp@potion-studios.com>

PORTNAME=		gcc
PORTVERSION=		4.9.3
PORTREVISION?=		2
CATEGORIES=		devel
MASTER_SITES=		GCC
PKGNAMEPREFIX=		psptoolchain-
PKGNAMESUFFIX?=		-stage1

MAINTAINER=		ports@FreeBSD.org
COMMENT=		PlayStation Portable development toolchain ${PORTNAME}

LICENSE=		GPLv3

ONLY_FOR_ARCHS=		aarch64 amd64 armv7 i386 powerpc powerpc64 powerpc64le

LIB_DEPENDS=		libgmp.so:math/gmp \
			libmpfr.so:math/mpfr \
			libmpc.so:math/mpc

PSP_GCC_STAGE_PREFIX=	psp/stage1

BUILD_DEPENDS+=		psp-addr2line:devel/psptoolchain-binutils \
			psp-ar:devel/psptoolchain-binutils \
			psp-as:devel/psptoolchain-binutils \
			psp-c++filt:devel/psptoolchain-binutils \
			psp-ld:devel/psptoolchain-binutils \
			psp-nm:devel/psptoolchain-binutils \
			psp-objcopy:devel/psptoolchain-binutils \
			psp-objdump:devel/psptoolchain-binutils \
			psp-ranlib:devel/psptoolchain-binutils \
			psp-readelf:devel/psptoolchain-binutils \
			psp-size:devel/psptoolchain-binutils \
			psp-strings:devel/psptoolchain-binutils \
			psp-strip:devel/psptoolchain-binutils \
			objdump:devel/binutils

USES+=			compiler:c11 cpe gmake libtool tar:bzip2
CPE_VENDOR=		gnu

MAKE_ENV+=		PATH=${LOCALBASE}/${PSP_GCC_STAGE_PREFIX}/bin:${PREFIX}/bin:${PATH}
HAS_CONFIGURE=		yes
CONFIGURE_OUTSOURCE=	yes
CONFIGURE_ARGS?=	--prefix=${PREFIX}/${PSP_GCC_STAGE_PREFIX} \
			--target="psp" \
			--enable-languages="c" \
			--enable-lto \
			--with-newlib \
			--with-gmp=${LOCALBASE} \
			--with-mpfr \
			--without-headers \
			--disable-libssp \
			--disable-nls \
			--with-ld=${LOCALBASE}/bin/psp-ld \
			--with-as=${LOCALBASE}/bin/psp-as \
			--mandir=${PREFIX}/man
CFLAGS+=		-Wno-reserved-user-defined-literal
SSP_CFLAGS?=		-fstack-protector # XXX -strong isn't supported by GCC < 4.9

# make sure xgcc doesn't get any -march=... from env C(XX)?FLAGS (e.g. set by CPUTYPE in make.conf); also "disable" info file gen
CONFIGURE_ENV+=		CFLAGS_FOR_TARGET="${CFLAGS:C/(^|[[:space:]])-march=[^[:space:]]*//g} ${XGCC_FLAGS}" \
			CXXFLAGS_FOR_TARGET="${CXXFLAGS:C/(^|[[:space:]])-march=[^[:space:]]*//g} ${XGCC_FLAGS}" \
			MAKEINFO=true

# Don't install any documentation for psptoolchain's gcc stage 1 - makes no sense.
# Disable installation of .info files and libiberty for both stages.
post-patch:
	@${REINPLACE_CMD} -E "s/^(install-data-am:)(.*)install-info-am(.*)/\1 \2 \3/" \
		${PATCH_WRKSRC}/libquadmath/Makefile.in
	@${REINPLACE_CMD} -E "s/^(install:)(.*)/\1#\2/" ${PATCH_WRKSRC}/libiberty/Makefile.in
	@${REINPLACE_CMD} -E \
		-e "/^	\\$$\(mkinstalldirs\) \\$$\(DESTDIR\)\\$$\((infodir|man7dir)\)/d" \
		-e "s/^(install-info:)(.*)/\1#\2/" \
		-e "/^	\\$$\(DESTDIR\)\\$$\(man7dir\)\/(fsf-funding|gfdl|gpl)\\$$\(man7ext\)/d" \
		${PATCH_WRKSRC}/gcc/Makefile.in
.if ${PKGNAMESUFFIX} == "-stage1"
	@${REINPLACE_CMD} -E "s/^(install-man:)(.*)/\1#\2/" ${PATCH_WRKSRC}/gcc/Makefile.in
.endif

PLIST_SUB+=		PSP_GCC_STAGE_PREFIX=${PSP_GCC_STAGE_PREFIX}

.include <bsd.port.mk>
