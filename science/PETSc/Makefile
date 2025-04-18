# Created by: Thierry Thomas <thierry@pompo.net>

PORTNAME=	PETSc
DISTVERSION=	3.16.3
CATEGORIES=	science devel
MASTER_SITES=	https://ftp.mcs.anl.gov/pub/petsc/release-snapshots/
DISTNAME=	${PORTNAME:tl}-${DISTVERSION}

MAINTAINER=	yuri@FreeBSD.org
COMMENT=	Suite of data structures and routines from Argonne National Laboratory

LICENSE=	BSD2CLAUSE
LICENSE_FILE=	${WRKSRC}/LICENSE

BUILD_DEPENDS=	cmake:devel/cmake
LIB_DEPENDS=	libmpich.so:net/mpich

USES=		blaslapack fortran gmake python:3.7+ shebangfix xorg
GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--with-shared-libraries=1 \
		--with-mpi-dir=${LOCALBASE} \
		--with-python=1 --with-python-pkg-config=${LOCALBASE}/libdata/pkgconfig \
		FCFLAGS="${FCFLAGS}" FFLAGS="${FCFLAGS}"	\
		${CONFIGURE_ARGS_${ARCH}} CPPFLAGS="${CPPFLAGS}" \
		AR=${AR} RANLIB=${RANLIB} \
		MAKEFLAGS="${MAKEFLAGS}" LDFLAGS="${LDFLAGS}" LIBS=""
CONFIGURE_ARGS_amd64=	CFLAGS="${CFLAGS} -msse2" CXXFLAGS="${CXXFLAGS} -msse2"
CONFIGURE_ARGS_i386=	CFLAGS="${CFLAGS} -msse2" CXXFLAGS="${CXXFLAGS} -msse2"
CONFIGURE_LOG=	configure.log
USE_XORG=	x11
MAKEFILE=	makefile
SHEBANG_FILES=	lib/petsc/bin/*.py lib/petsc/bin/saws/SAWs.py lib/petsc/bin/saws/*.bash config/*.py	\
		lib/petsc/bin/petscnagfor lib/petsc/bin/petsc-performance-view
USE_LDCONFIG=	yes
TEST_TARGET=	test
BINARY_ALIAS=	python=${PYTHON_CMD}

LDFLAGS+=	${LOCALBASE}/lib/libmpi.so

DATADIR=	${PREFIX}/share/${PORTNAME:tl}
PLIST_SUB=	SHLIB=${DISTVERSION} SHL=${DISTVERSION:C/\.[0-9]$//}

pre-configure:
	${REINPLACE_CMD} -e 's|python3|${PYTHON_CMD}|' ${WRKSRC}/${CONFIGURE_SCRIPT}

post-install:
	@${STRIP_CMD} ${STAGEDIR}${PREFIX}/lib/libpetsc.so.${DISTVERSION}
	@${FIND} ${STAGEDIR}${PREFIX} -name "*.html" -delete
	@cd ${STAGEDIR}${PREFIX} && ${RM} -r bin/win32fe lib/petsc/conf/uninstall.py
	@${REINPLACE_CMD} -i '' -e 's|^PYTHON = .*|PYTHON = ${PYTHON_CMD}|' ${STAGEDIR}${PREFIX}/lib/petsc/conf/petscvariables
	@${REINPLACE_CMD} -i '' -e 's|#!/.*|#!${PYTHON_CMD}|' ${STAGEDIR}${PREFIX}/lib/petsc/conf/reconfigure-arch-*-c-debug.py
	@${RM} -r ${STAGEDIR}${DATADIR}/examples # examples are a mess as installed

.include <bsd.port.mk>
