# Created by: Devon H. O'Dell <devon.odell@gmail.com>

PORTNAME=	go
PORTVERSION?=	1.17.6
PORTREVISION?=	0
PORTEPOCH?=	1
CATEGORIES=	lang
MASTER_SITES?=	https://golang.org/dl/ \
		https://github.com/dmgk/go-bootstrap/releases/download/${BOOTSTRAP_TAG}/:bootstrap \
		LOCAL/dmgk:bootstrap
DISTFILES?=	go${PORTVERSION}.src.tar.gz \
		go-${OPSYS:tl}-${GOARCH_${ARCH}}${GOARM_${ARCH}}-${BOOTSTRAP_TAG}.tar.xz:bootstrap

MAINTAINER=	ygy@FreeBSD.org
COMMENT?=	Go programming language

LICENSE=	BSD3CLAUSE
LICENSE_FILE=	${WRKSRC}/LICENSE

.ifdef QEMU_EMULATING
IGNORE=		fails to build with qemu-user-static
.endif

ONLY_FOR_ARCHS=	aarch64 amd64 armv6 armv7 i386

RUN_DEPENDS=	${RUN_DEPENDS_${ARCH}}
# ld.bfd from devel/binutils is needed for working cgo on aarch64
RUN_DEPENDS_aarch64=	binutils>0:devel/binutils

TEST_DEPENDS=	${TEST_DEPENDS_${ARCH}}
TEST_DEPENDS_aarch64=	binutils>0:devel/binutils

USES=		cpe shebangfix

CPE_VENDOR=	golang

SHEBANG_FILES=	misc/wasm/go_js_wasm_exec \
		src/net/http/cgi/testdata/test.cgi
SHEBANG_GLOB=	*.bash *.pl *.sh

CONFLICTS_INSTALL?=	go-devel

# Upstream archive contains files with UTF-8 names
EXTRACT_CMD=	${SETENV} LC_ALL=en_US.UTF-8 ${TAR}

.ifndef MASTERDIR
WRKSRC=		${WRKDIR}/go
.endif

OPTIONS_DEFINE_i386=	SOFTFLOAT

SOFTFLOAT_DESC=	Use soft float on non-SSE2 processors (Pentium 4 and older)

SOFTFLOAT_VARS=	GO386=softfloat

BINARIES=	go gofmt
BOOTSTRAP_TAG=	go1.14

GOARCH_aarch64=	arm64
GOARCH_amd64=	amd64
GOARCH_armv6=	arm
GOARCH_armv7=	arm
GOARCH_i386=	386

GOARM_armv6=	6
GOARM_armv7=	7

post-patch:
	@${REINPLACE_CMD} -e 's|^if ulimit -T|false \&\& &|' ${WRKSRC}/src/run.bash

pre-build:
	# Check that the running kernel has COMPAT_FREEBSD11 required by lang/go{,-devel} post-ino64
	@${SETENV} CC="${CC}" OPSYS="${OPSYS}" OSVERSION="${OSVERSION}" WRKDIR="${WRKDIR}" \
		${SH} ${SCRIPTSDIR}/rust-compat11-canary.sh

do-build:
	cd ${WRKSRC}/src ; ${SETENV} \
		XDG_CACHE_HOME=${WRKDIR} \
		GOROOT_BOOTSTRAP=${WRKDIR}/go-${OPSYS:tl}-${GOARCH_${ARCH}}${GOARM_${ARCH}}-bootstrap \
		GOROOT=${WRKSRC} \
		GOROOT_FINAL=${PREFIX}/go \
		GOBIN= \
		GOOS=${OPSYS:tl} \
		GOARCH=${GOARCH_${ARCH}} \
		GO386=${GO386} \
		GOARM=${GOARM_${ARCH}} \
		CC=${CC} \
		${SH} make.bash -v

do-install:
	@cd ${WRKSRC} ; \
		${RM} -r .gitattributes .gitignore .github favicon.ico robots.txt \
		pkg/obj pkg/bootstrap pkg/${OPSYS:tl}_${GOARCH_${ARCH}}/cmd
	@${MKDIR} ${STAGEDIR}${PREFIX}/go
	@${CP} -a ${WRKSRC}/* ${STAGEDIR}${PREFIX}/go
.for file in ${BINARIES}
	@${LN} -sf ../go/bin/${file} ${STAGEDIR}${PREFIX}/bin/${file}
	@${ECHO_CMD} bin/${file} >> ${TMPPLIST}
.endfor
	@cd ${STAGEDIR}${PREFIX} && ${FIND} go -type f >> ${TMPPLIST}

do-test:
	cd ${WRKSRC}/src && ${SETENV} \
		GOROOT=${WRKSRC} \
		PATH=${WRKSRC}/bin:${PATH} \
		GOOS=${OPSYS:tl} \
		GOARCH=${GOARCH_${ARCH}} \
		GO386=${GO386} \
		GOARM=${GOARM_${ARCH}} \
		CC=${CC} \
		${SH} run.bash -no-rebuild

.if !defined(_GO_MAKESUM_GUARD)
makesum:
	${MAKE} -D_GO_MAKESUM_GUARD makesum ARCH=${ONLY_FOR_ARCHS:O:[1]} DISTINFO_FILE=${DISTINFO_FILE}.tmp
.for arch in ${ONLY_FOR_ARCHS:O:[2..-1]}
	${MAKE} -D_GO_MAKESUM_GUARD makesum ARCH=${arch} DISTINFO_FILE=${DISTINFO_FILE}.${arch}
	${SED} 1d ${DISTINFO_FILE}.${arch} >> ${DISTINFO_FILE}.tmp
	${RM} ${DISTINFO_FILE}.${arch}
.endfor
	${AWK} '!seen[$$0]++' ${DISTINFO_FILE}.tmp > ${DISTINFO_FILE}
	${RM} ${DISTINFO_FILE}.tmp
.endif

.include <bsd.port.mk>
