PORTNAME=	mongodb
DISTVERSIONPREFIX=	r
DISTVERSION=	4.2.18
CATEGORIES=	databases net
MASTER_SITES=	https://fastdl.mongodb.org/src/ \
		http://fastdl.mongodb.org/src/
PKGNAMESUFFIX=	${DISTVERSION:R:S/.//}
DISTNAME=	mongodb-src-${DISTVERSIONPREFIX}${DISTVERSION}

PATCH_SITES=	https://github.com/${PORTNAME}/${PORTNAME:S/db//}/commit/
PATCHFILES+=	a0a70c53cc7a.patch:-p1 # https://jira.mongodb.org/browse/SERVER-41827
PATCHFILES+=	edf4ab0f8174.patch:-p1 # https://jira.mongodb.org/browse/SERVER-43979

MAINTAINER=	ronald-lists@klop.ws
COMMENT=	Distributed document-oriented "NoSQL" database (4.2.x Branch)

LICENSE=	SSPLv1 APACHE20 # mongodb is SSPLv1, C++ driver is APACHE20
LICENSE_COMB=	multi
LICENSE_NAME_SSPLv1=	Server Side Public License
LICENSE_FILE_SSPLv1=	${WRKSRC}/LICENSE-Community.txt
LICENSE_PERMS_SSPLv1=	dist-mirror dist-sell pkg-mirror pkg-sell auto-accept

ONLY_FOR_ARCHS=	aarch64 amd64 powerpc64le
ONLY_FOR_ARCHS_REASON=	only ported to amd64, aarch64, and powerpc64le on FreeBSD; upstream supports arm64, ppc64le, s390x, and x86-64

BUILD_DEPENDS=	${PYTHON_PKGNAMEPREFIX}cheetah3>0:devel/py-cheetah3@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}yaml>=3.11:devel/py-yaml@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}psutil>0:sysutils/py-psutil@${PY_FLAVOR} \
		${LOCALBASE}/bin/ar:devel/binutils
LIB_DEPENDS=	libboost_system.so:devel/boost-libs \
		libpcre.so:devel/pcre \
		libcurl.so:ftp/curl \
		libsnappy.so:archivers/snappy

USES=		compiler:c++17-lang cpe python:3.5+,build scons shebangfix
USE_RC_SUBR=	mongod

CONFLICTS_INSTALL=	mongodb36 mongodb4[04] mongodb50

OPTIONS_DEFINE=	LTO SASL SSL
OPTIONS_DEFAULT=LTO SASL SSL
OPTIONS_EXCLUDE_aarch64=        ${OPTIONS_EXCLUDE_${ARCH}_${OSREL:R}}
OPTIONS_EXCLUDE_aarch64_14=     LTO # Does not work with llvm12 on aarch64.

SHEBANG_FILES=	src/mongo/installer/compass/install_compass
python_OLD_CMD=	@python_interpreter@

MAKE_ARGS=	--prefix=${STAGEDIR}${PREFIX} \
		--use-system-zlib \
		--use-system-pcre \
		--use-system-snappy \
		--use-system-boost \
		--libc++ \
		--cxx-std=17 \
		--runtime-hardening=on \
		-j ${MAKE_JOBS_NUMBER} \
		--disable-warnings-as-errors \
		VERBOSE=on \
		AR=${PREFIX}/bin/ar

USERS=		mongodb
GROUPS=		mongodb

LTO_MAKE_ARGS=	--lto=on

SASL_LIB_DEPENDS=	libsasl2.so:security/cyrus-sasl2
SASL_MAKE_ARGS=		--use-sasl-client

SSL_USES=	ssl
SSL_MAKE_ARGS=	--ssl

.include <bsd.port.pre.mk>

.if ${ARCH} == aarch64 || ${ARCH} == powerpc64le
EXTRA_PATCHES=	${FILESDIR}/${ARCH}
.endif

ALL_TARGET=	core

PORTSCOUT=	limitw:1,even

CPE_PRODUCT=	mongodb

pre-patch:
	${MV} ${WRKSRC}/src/third_party/wiredtiger/src/checksum/power8/crc32.sx ${WRKSRC}/src/third_party/wiredtiger/src/checksum/power8/crc32.S

post-install:
.for f in mongo mongod mongos
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/bin/${f}
.endfor
	${CP} ${WRKSRC}/rpm/mongod.conf ${STAGEDIR}${PREFIX}/etc/mongodb.conf.sample

.include <bsd.port.post.mk>
