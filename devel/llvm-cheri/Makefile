PORTNAME=	llvm
PORTVERSION=	${LLVM_MAJOR}.0.d${SNAPDATE}
PORTREVISION=	0
CATEGORIES=	devel lang
PKGNAMESUFFIX=	${LLVM_SUFFIX}

MAINTAINER=	brooks@FreeBSD.org
COMMENT?=	LLVM and Clang with support for the CHERI architecture

LICENSE_DIR=	${WRKSRC}/llvm
.include "${.PARSEDIR}/../llvm-devel/Makefile.LICENSE"
LICENSE:=       ${LICENSE:NARM}
LICENSE+=	LLVM2
LICENSE_FILE_LLVM2=	${LICENSE_DIR}/LICENSE.TXT
LICENSE_NAME_LLVM2=	Apache License 2.0 with LLVM Exceptions
LICENSE_PERMS_LLVM2=	dist-mirror dist-sell pkg-mirror pkg-sell auto-accept

NOT_FOR_ARCHS=		i386 armv6 armv7 powerpc mips
NOT_FOR_ARCHS_REASON=	No one will develop CHERI from 32-bit

LLVM_SUFFIX?=	-cheri
LLVM_PREFIX=	${PREFIX}/llvm${LLVM_SUFFIX}
COMMAND_SUFFIX=	${LLVM_SUFFIX}
DOCSDIR=	${PREFIX}/share/doc/${PORTNAME}${LLVM_SUFFIX}
DATADIR=	${PREFIX}/share/${PORTNAME}${LLVM_SUFFIX}

USES=		cmake compiler:c++11-lib cpe libedit perl5 \
		shebangfix
USE_LDCONFIG=	${LLVM_PREFIX}/lib
SHEBANG_FILES=	llvm/utils/lit/lit.py \
		llvm/utils/llvm-lit/llvm-lit.in \
		clang/utils/hmaptool/hmaptool \
		clang/tools/scan-view/bin/scan-view \
		clang/tools/clang-format/git-clang-format \
		clang/tools/clang-format/clang-format-diff.py \
		llvm/tools/opt-viewer/optrecord.py \
		llvm/tools/opt-viewer/opt-diff.py \
		llvm/tools/opt-viewer/opt-stats.py \
		llvm/tools/opt-viewer/opt-viewer.py

SUB_FILES=	llvm-wrapper.sh
SUB_LIST=	LLVM_PREFIX="${LLVM_PREFIX}" LLVM_SUFFIX="${LLVM_SUFFIX}"

CMAKE_INSTALL_PREFIX=	${LLVM_PREFIX}
CMAKE_SOURCE_PATH=	${WRKSRC}/llvm
CMAKE_ARGS+=	-DLLVM_BUILD_LLVM_DYLIB=ON -DLLVM_LINK_LLVM_DYLIB=ON
CMAKE_ARGS+=	-DCMAKE_INSTALL_MANDIR:PATH="share/man"
CMAKE_ARGS+=	-DLLVM_PARALLEL_LINK_JOBS=1
CMAKE_ARGS+=	-DLLVM_ENABLE_Z3_SOLVER=OFF
CMAKE_ARGS+=	-DLLVM_TARGETS_TO_BUILD="${LLVM_TARGETS}"

.ifndef MASTERDIR
USE_GITHUB=	yes
GH_PROJECT=	llvm-project
GH_ACCOUNT=	CTSRD-CHERI
GH_TAGNAME=	${LLVM_COMMIT}
.endif

.sinclude "${.CURDIR}/Makefile.snapshot"

OPTIONS_DEFINE=	CLANG DOCS LIT LLD
OPTIONS_DEFAULT=	CLANG LIT LLD
OPTIONS_SUB=	yes

CLANG_DESC=		Build clang
CLANG_PORTDOCS=		clang
PLIST_FILES+=		share/toolchains/llvm${LLVM_SUFFIX}.mk
SUB_FILES+=		xtoolchain.mk
CLANG_USE=		GNOME=libxml2
DOCS_BUILD_DEPENDS=	${PYTHON_PKGNAMEPREFIX}sphinx>=0,1:textproc/py-sphinx@${PY_FLAVOR} \
			${PYTHON_PKGNAMEPREFIX}recommonmark>=0.0.20180530:textproc/py-recommonmark@${PY_FLAVOR}
DOCS_CMAKE_ON=		-DLLVM_ENABLE_SPHINX=ON \
			-DSPHINX_EXECUTABLE=${LOCALBASE}/bin/sphinx-build-${PYTHON_VER} \
			-DSPHINX_WARNINGS_AS_ERRORS=OFF \
			-DLLVM_BUILD_DOCS=ON
DOCS_PLIST_FILES=	${MAN1SRCS:S|^|man/man1/|:S|.1$|${LLVM_SUFFIX}.1.gz|}
DOCS_PORTDOCS=		llvm
LIT_DESC=		Install lit and FileCheck test tools
LLD_DESC=		Install lld linker
LLD_PORTDOCS=		lld
LLDB_DESC=		Install lldb, the LLVM debugger
LLDB_BUILD_DEPENDS=	swig:devel/swig

LLVM_TARGETS?=		AArch64;ARM;Mips;PowerPC;RISCV;X86

PLIST_SUB+=	COMMAND_SUFFIX=${COMMAND_SUFFIX} \
		LLVM_MAJOR=${LLVM_MAJOR} \
		LLVM_RELEASE=${LLVM_RELEASE} \
		LLVM_SUFFIX=${LLVM_SUFFIX}

COMMANDS=	${LLVM_COMMANDS}
FIRST_COMMAND=	${COMMANDS:C/^/XXXX/1:MXXXX*:C/^XXXX//}

STRIP_LIBS=	BugpointPasses.so \
		LLVMHello.so \
		${LIBNAME}.0 \
		libLTO.so

.include <bsd.port.options.mk>

# keep in sync with /usr/src/lib/clang/clang.build.mk
CONFIGURE_TARGET:=${ARCH:C/amd64/x86_64/:C/armv6hf/armv6/}-portbld-${OPSYS:tl}${OSREL}

.if ${PORT_OPTIONS:MCLANG}
LLVM_ENABLE_PROJECTS+=	clang
COMMANDS+=	${CLANG_COMMANDS}
MAN1SRCS+=	clang.1 \
		clang-tblgen.1 \
		diagtool.1 \
		scan-build.1
#DOCS_PLIST_FILES+=	man/man1/scan-build${LLVM_SUFFIX}.1.gz
USES+=		gnome
.endif

.if ${PORT_OPTIONS:MLIT}
MAN1SRCS+=	lit.1 FileCheck.1
_USES_PYTHON=	python:3.6+
.endif

.if ${PORT_OPTIONS:MLLD}
LLVM_ENABLE_PROJECTS+=	lld
COMMANDS+=	${LLD_COMMANDS}
.endif

.if ${PORT_OPTIONS:MLLDB}
LLVM_ENABLE_PROJECTS+=	lldb
COMMANDS+=	${LLDB_COMMANDS}
MAN1SRCS+=	lldb-tblgen.1
_USES_PYTHON=	python:3.6+
.endif

.if defined(LLVM_ENABLE_PROJECTS)
CMAKE_ARGS+=	-DLLVM_ENABLE_PROJECTS="${LLVM_ENABLE_PROJECTS:ts;}"
.endif

_USES_PYTHON?=	python:3.6+,build
USES+=		${_USES_PYTHON}

MAN1SRCS+=	bugpoint.1 \
		dsymutil.1 \
		llc.1 \
		lli.1 \
		llvm-addr2line.1 \
		llvm-ar.1 \
		llvm-as.1 \
		llvm-bcanalyzer.1 \
		llvm-config.1 \
		llvm-cov.1 \
		llvm-cxxfilt.1 \
		llvm-cxxmap.1 \
		llvm-diff.1 \
		llvm-dis.1 \
		llvm-dwarfdump.1 \
		llvm-exegesis.1 \
		llvm-extract.1 \
		llvm-install-name-tool.1 \
		llvm-lib.1 \
		llvm-libtool-darwin.1 \
		llvm-link.1 \
		llvm-lipo.1 \
		llvm-locstats.1 \
		llvm-mca.1 \
		llvm-nm.1 \
		llvm-objcopy.1 \
		llvm-objdump.1 \
		llvm-otool.1 \
		llvm-pdbutil.1 \
		llvm-profdata.1 \
		llvm-profgen.1 \
		llvm-ranlib.1 \
		llvm-readelf.1 \
		llvm-readobj.1 \
		llvm-size.1 \
		llvm-stress.1 \
		llvm-strings.1 \
		llvm-strip.1 \
		llvm-symbolizer.1 \
		llvm-tblgen.1 \
		opt.1 \
		tblgen.1

.include <bsd.port.pre.mk>
.include "${.CURDIR}/Makefile.COMMANDS"

post-patch:
	${REINPLACE_CMD} -e 's|import lit|import lit${LLVM_SUFFIX}|' \
	    -e 's|from lit|from lit${LLVM_SUFFIX}|' \
	    -e 's|lit\.|lit${LLVM_SUFFIX}.|' \
	    ${WRKSRC}/llvm/utils/lit/lit.py ${WRKSRC}/llvm/utils/lit/lit/*.py

post-patch-LLD-on:
		${REINPLACE_CMD} -e "s|'indexsidebar.html'|['indexsidebar.html']|" \
			${PATCH_WRKSRC}/lld/docs/conf.py

post-install:
	${MKDIR} ${STAGEDIR}${PREFIX}/share/toolchains/
	${INSTALL_DATA} ${WRKDIR}/xtoolchain.mk \
	    ${STAGEDIR}${PREFIX}/share/toolchains/llvm${LLVM_SUFFIX}.mk
	${INSTALL_SCRIPT} ${WRKDIR}/llvm-wrapper.sh \
	    ${STAGEDIR}${PREFIX}/bin/${COMMAND_PREFIX}${FIRST_COMMAND}${COMMAND_SUFFIX}
.for command in ${COMMANDS:C/^/XXXX/1:NXXXX*}
	${LN} -f ${STAGEDIR}${PREFIX}/bin/${COMMAND_PREFIX}${FIRST_COMMAND}${COMMAND_SUFFIX} \
	    ${STAGEDIR}${PREFIX}/bin/${COMMAND_PREFIX}${command}${COMMAND_SUFFIX}
.endfor
	${RMDIR} ${STAGEDIR}${LLVM_PREFIX}/include/llvm/CHERI/cheri-compressed-cap/.github/workflows
	${RMDIR} ${STAGEDIR}${LLVM_PREFIX}/include/llvm/CHERI/cheri-compressed-cap/.github

post-install-DOCS-on:
	${MV} ${STAGEDIR}${LLVM_PREFIX}/share/doc ${STAGEDIR}${DOCSDIR}
.for _man in ${MAN1SRCS}
	${MV} ${STAGEDIR}${LLVM_PREFIX}/share/man/man1/${_man} \
	    ${STAGEDIR}${MANPREFIX}/man/man1/${_man:R}${LLVM_SUFFIX}.1
.endfor
.if ! ${PORT_OPTIONS:MLIT}
	${RM} ${STAGEDIR}${LLVM_PREFIX}/share/man/man1/lit.1
	${RM} ${STAGEDIR}${LLVM_PREFIX}/share/man/man1/FileCheck.1
.endif
#.if ${PORT_OPTIONS:MCLANG}
#	${MV} ${STAGEDIR}${LLVM_PREFIX}/share/man/man1/scan-build.1 \
#	    ${STAGEDIR}${MANPREFIX}/man/man1/scan-build${LLVM_SUFFIX}.1
#.endif
.if !${PORT_OPTIONS:MLLDB}
	${RM} ${STAGEDIR}${LLVM_PREFIX}/share/man/man1/lldb-tblgen.1
.endif
	${RM} ${STAGEDIR}${LLVM_PREFIX}/share/man/man1/mlir-tblgen.1
	${RMDIR} ${STAGEDIR}${LLVM_PREFIX}/share/man/man1/
	${RMDIR} ${STAGEDIR}${LLVM_PREFIX}/share/man/

post-install-LLDB-on:
.if ${OPSYS} != "FreeBSD" || ${COMPILER_TYPE} == clang
	${RM} ${STAGEDIR}${LLVM_PREFIX}/lib/python*/site-packages/lib
.endif

post-install-CLANG-on:
	${LN} -f ${STAGEDIR}${LLVM_PREFIX}/bin/clang \
	    ${STAGEDIR}${LLVM_PREFIX}/bin/clang-cpp

post-install-LIT-on:
	${INSTALL_SCRIPT} ${PATCH_WRKSRC}/llvm/utils/lit/lit.py \
	    ${STAGEDIR}${LLVM_PREFIX}/bin/lit
	${LN} -f ${STAGEDIR}${LLVM_PREFIX}/bin/lit \
	    ${STAGEDIR}${LLVM_PREFIX}/bin/llvm-lit
	${LN} -f ${STAGEDIR}${LLVM_PREFIX}/bin/lit \
	    ${STAGEDIR}${PREFIX}/bin/${COMMAND_PREFIX}lit${COMMAND_SUFFIX}
	${LN} -f ${STAGEDIR}${LLVM_PREFIX}/bin/lit \
	    ${STAGEDIR}${PREFIX}/bin/${COMMAND_PREFIX}llvm-lit${COMMAND_SUFFIX}
	${MKDIR} ${STAGEDIR}${PYTHONPREFIX_SITELIBDIR}/lit${LLVM_SUFFIX}
	${INSTALL_DATA} ${WRKSRC}/llvm/utils/lit/lit/*.py \
	    ${STAGEDIR}${PYTHONPREFIX_SITELIBDIR}/lit${LLVM_SUFFIX}
	${INSTALL_PROGRAM} ${WRKDIR}/.build/bin/FileCheck \
	    ${STAGEDIR}${LLVM_PREFIX}/bin/
	${LN} -f ${STAGEDIR}${LLVM_PREFIX}/bin/FileCheck \
	    ${STAGEDIR}${PREFIX}/bin/${COMMAND_PREFIX}FileCheck${COMMAND_SUFFIX}

TEST_CMD=	'(cd ${WRKSRC}/llvm/test; ${SETENV} ${MAKE_ENV} LD_LIBRARY_PATH=${WRKSRC}/Release/lib ${MAKE_CMD} check-local-lit)'
do-test:
	if [ `${ID} -u` = 0 ]; then \
		${CHOWN} -R nobody ${WRKSRC}/llvm/test; \
		su -m nobody -c ${TEST_CMD}; \
	else \
		${SH} -c ${TEST_CMD}; \
	fi

build-plist:
	${RM} ${PLIST} ${PLIST}.tmp
.for command in ${COMMANDS}
	${ECHO_CMD} bin/${COMMAND_PREFIX}${command}%%COMMAND_SUFFIX%% >> ${PLIST}.tmp
.endfor
.for command in ${LIT_COMMANDS}
	${ECHO_CMD} %%LIT%%bin/${COMMAND_PREFIX}${command}%%COMMAND_SUFFIX%% >> ${PLIST}.tmp
	${ECHO_CMD} %%LIT%%${LLVM_PREFIX:S|${PREFIX}/||:S|${LLVM_SUFFIX}|%%LLVM_SUFFIX%%|}/bin/${command} >> ${PLIST}.tmp
.endfor
	${FIND} ${STAGEDIR}${LLVM_PREFIX} -type f -o -type l | \
	    ${GREP} -v '[/-]lit$$' | ${GREP} -v 'FileCheck$$' | \
	    ${GREP} -v man/man1 | ${SED} -e 's|${STAGEDIR}${PREFIX}/||' \
	    -e 's|${PORTVERSION}|%%PORTVERSION%%|' \
	    -e 's|release.cmake|%%CMAKE_BUILD_TYPE%%.cmake|' \
	    -e 's|${LLVM_RELEASE:C/\./\\./g}|%%LLVM_RELEASE%%|' \
	    -e 's|${LLVM_MAJOR:C/\./\\./}|%%LLVM_MAJOR%%|' \
	    -e 's|${LLVM_SUFFIX}|%%LLVM_SUFFIX%%|' \
	    | ${SORT} >> ${PLIST}.tmp
	${FIND} ${STAGEDIR}${PYTHON_SITELIBDIR}/lit${LLVM_SUFFIX} -type f | \
	    ${SED} -e 's|${STAGEDIR}${PYTHON_SITELIBDIR}|%%LIT%%%%PYTHON_SITELIBDIR%%|' \
	    -e 's|${LLVM_RELEASE:C/\./\\./g}|%%LLVM_RELEASE%%|' \
	    -e 's|${LLVM_MAJOR:C/\./\\./}|%%LLVM_MAJOR%%|' \
	    -e 's|${LLVM_SUFFIX}|%%LLVM_SUFFIX%%|' \
	    | ${SORT} >> ${PLIST}.tmp
	awk '{ \
	    if ($$0 ~ /clang/ && $$0 !~ /omp.h/) {printf "%%%%CLANG%%%%"} \
	    if ($$0 ~ /lld|wasm-ld/ && $$0 !~ /lldb/) {printf "%%%%LLD%%%%"} \
	    if ($$0 ~ /(argdumper|lldb)/) {printf "%%%%LLDB%%%%"} \
	    print \
	}' \${PLIST}.tmp >> ${PLIST}
	${ECHO_CMD} '@postexec if type ccache-update-links >/dev/null 2>&1; then ccache-update-links -v; fi' >> ${PLIST}
	${ECHO_CMD} '@postunexec if type ccache-update-links >/dev/null 2>&1; then ccache-update-links -v; fi' >> ${PLIST}
	${RM} ${PLIST}.tmp

check-commands:
.for command in ${COMMANDS}
	test -e ${STAGEDIR}${LLVM_PREFIX}/bin/${command}
.endfor

.include <bsd.port.post.mk>
