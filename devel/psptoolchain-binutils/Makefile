# Created by: Tassilo Philipp <tphilipp@potion-studios.com>

PORTNAME=	binutils
PORTVERSION=	2.22
PORTREVISION=	1
CATEGORIES=	devel
MASTER_SITES=	GNU \
		SOURCEWARE/${PORTNAME}/releases
PKGNAMEPREFIX=	psptoolchain-

MAINTAINER=	ports@FreeBSD.org
COMMENT=	PlayStation Portable development toolchain ${PORTNAME}

LICENSE=	GPLv3 LGPL3
LICENSE_COMB=	multi

BROKEN_mips64=		fails to package: ansidecl.h: No such file or directory

USES=		cpe gmake tar:bzip2 libtool
CPE_VENDOR=	gnu

HAS_CONFIGURE=	yes
CONFIGURE_TARGET=	${ARCH:S/aarch64/arm64/:S/amd64/x86_64/:C/armv[0-9]+/arm/:C/powerpc64.*/powerpc/:S/riscv64/riscv/}-unknown-${OPSYS:tl}${OSREL}
CONFIGURE_ARGS=	--prefix=${PREFIX} \
		--target="psp" \
		--enable-install-libbfd \
		--disable-werror \
		--disable-nls \
		--mandir=${PREFIX}/man
PLIST_SUB=	CONFIGURE_TARGET="${CONFIGURE_TARGET}"

# Disable installation of .info files and libiberty.
post-patch:
	@${REINPLACE_CMD} -E 's/^(install-data-am:)(.*)install-info-am(.*)/\1 \2 \3/' \
		${WRKSRC}/ld/Makefile.in
	@${REINPLACE_CMD} -E 's/^(install-info:)(.*install-info-am.*)/\1#\2/' \
		${WRKSRC}/gas/doc/Makefile.in \
		${WRKSRC}/bfd/doc/Makefile.in \
		${WRKSRC}/binutils/doc/Makefile.in
	@${REINPLACE_CMD} -E 's/^(install:)(.*)/\1#\2/' ${WRKSRC}/libiberty/Makefile.in
	@${REINPLACE_CMD} -E 's,^(install.*:)(.*)install-info(.*),\1 \2 \3,' ${WRKSRC}/etc/Makefile.in

.include <bsd.port.mk>
