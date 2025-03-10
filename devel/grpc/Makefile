# Created by: vanilla@

PORTNAME=	grpc
PORTVERSION=	1.42.0
DISTVERSIONPREFIX=	v
PORTEPOCH=	2
CATEGORIES=	devel

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	HTTP/2-based RPC framework

LICENSE=	BSD3CLAUSE
LICENSE_FILE=	${WRKSRC}/LICENSE

LIB_DEPENDS=	libabsl_base.so:devel/abseil \
		libbenchmark.so:devel/benchmark \
		libcares.so:dns/c-ares \
		libgflags.so:devel/gflags \
		libprotobuf.so:devel/protobuf \
		libre2.so:devel/re2

USES=		cmake compiler:c++17-lang cpe localbase:ldflags pkgconfig ssl

USE_GITHUB=	yes

CMAKE_ARGS=	-DCMAKE_CXX_STANDARD=17 \
		-DgRPC_ABSL_PROVIDER=package \
		-DgRPC_BENCHMARK_PROVIDER=package \
		-DgRPC_CARES_PROVIDER=package \
		-DgRPC_GFLAGS_PROVIDER=package \
		-DgRPC_PROTOBUF_PROVIDER=package \
		-DgRPC_RE2_PROVIDER=package \
		-DgRPC_SSL_PROVIDER=package \
		-DgRPC_ZLIB_PROVIDER=package
CMAKE_ON=	BUILD_SHARED_LIBS
USE_LDCONFIG=	yes

PLIST_SUB=	SHLIB_MAJOR=${PORTVERSION:R} \
		SHLIB_MINOR=${PORTVERSION:E}

.include <bsd.port.pre.mk>

# Remove openssl from grpc.pc because we do not ship openssl.pc in base system
.if ${SSL_DEFAULT} == base
EXTRA_PATCHES+=	${PATCHDIR}/extra-patch-CMakeLists.txt
.endif

post-patch:
# Clean up bundled libraries
	@${RM} -r ${WRKSRC}/third_party/abseil-cpp/
	@${RM} -r ${WRKSRC}/third_party/benchmark/
	@${RM} -r ${WRKSRC}/third_party/boringssl-with-bazel/
	@${RM} -r ${WRKSRC}/third_party/cares/
	@${RM} -r ${WRKSRC}/third_party/protobuf/
	@${RM} -r ${WRKSRC}/third_party/re2/
	@${RM} -r ${WRKSRC}/third_party/zlib/

.include <bsd.port.post.mk>
