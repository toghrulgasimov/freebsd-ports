# Created by: Sergey Skvortsov <skv@protey.ru>

PORTNAME=	redis5
PORTVERSION=	5.0.14
PORTREVISION=	1
CATEGORIES=	databases
MASTER_SITES=	https://download.redis.io/releases/
DISTNAME=	redis-${PORTVERSION}

MAINTAINER=	yasu@FreeBSD.org
COMMENT=	Persistent key-value database with built-in net interface

LICENSE=	BSD3CLAUSE
LICENSE_FILE=	${WRKSRC}/COPYING

DEPRECATED=	EOLed upstream
EXPIRATION_DATE=2022-03-31

OPTIONS_DEFINE=	JEMALLOC TESTS TRIB
OPTIONS_RADIO=	EXTLUA
OPTIONS_RADIO_EXTLUA=	LUA LUAJIT LUAJITOR
OPTIONS_SUB=	yes
JEMALLOC_DESC=	Use jemalloc
LUA_DESC=	Use lang/lua instead of builtin lua
LUAJIT_DESC=	Use lang/luajit instead of builtin lua
LUAJITOR_DESC=	Use lang/luajit-openjit instead of builtin lua
TESTS_DESC=	Install lang/tcl for redis unit tests
TRIB_DESC=	Install redis-trib.rb (lang/ruby req.)

USES+=		compiler:c11 gmake
MAKE_ENV=	"V=yo"

.include <bsd.port.options.mk>

.if ${ARCH} == i386 && ! ${CFLAGS:M-march=*}
# Needed for __atomic_fetch_add_8
USE_GCC=	yes
CFLAGS+=	-march=i586
.endif

.if ${PORT_OPTIONS:MJEMALLOC}
MAKE_ENV+=	"USE_JEMALLOC=yes"
.endif

.if ${PORT_OPTIONS:MTRIB}
CATEGORIES+=	ruby
USE_RUBY=	yes
RUN_DEPENDS=	rubygem-redis>=2.2:databases/rubygem-redis
.endif

.if ${PORT_OPTIONS:MLUA}
USES+=		lua:51
EXTRA_PATCHES+=	${PATCHDIR}/extra-patch-src-Makefile.lua
.endif

.if ${PORT_OPTIONS:MLUAJIT}
LIB_DEPENDS+=	libluajit-5.1.so:lang/luajit
EXTRA_PATCHES+=	${PATCHDIR}/extra-patch-src-Makefile.luajit
.endif

.if ${PORT_OPTIONS:MLUAJITOR}
LIB_DEPENDS+=	libluajit-5.1.so:lang/luajit-openresty
EXTRA_PATCHES+=	${PATCHDIR}/extra-patch-src-Makefile.luajit-or \
		${PATCHDIR}/extra-patch-deps_lua_src_lua__cjson.c
.endif

.if ${PORT_OPTIONS:MLUA} || ${PORT_OPTIONS:MLUAJIT} || ${PORT_OPTIONS:MLUAJITOR}
CFLAGS+=	-fPIC
LDFLAGS+=	-Wl,-E
.endif

.if ${PORT_OPTIONS:MTESTS}
USES+=		tcl:build
.endif

LDFLAGS+=	-lpthread -lm -lexecinfo

CONFLICTS?=	redis-6.* redis-devel-6.* redis6-6.*

USE_RC_SUBR=	redis sentinel
BIN_FILES=	redis-benchmark redis-check-aof redis-check-rdb \
		redis-cli redis-sentinel redis-server

USERS=	redis
GROUPS=	redis

REDIS_DBDIR?=	/var/db/redis
REDIS_RUNDIR?=	/var/run/redis
REDIS_LOGDIR?=	/var/log/redis

SUB_FILES=	pkg-message
SUB_LIST+=	PORTNAME=${PORTNAME} \
	REDIS_USER=${USERS} \
	REDIS_DBDIR=${REDIS_DBDIR} \
	REDIS_LOGDIR=${REDIS_LOGDIR} \
	REDIS_RUNDIR=${REDIS_RUNDIR}

PLIST_SUB+=	REDIS_USER=${USERS} \
	REDIS_GROUP=${GROUPS} \
	REDIS_LOGDIR=${REDIS_LOGDIR} \
	REDIS_DBDIR=${REDIS_DBDIR} \
	REDIS_RUNDIR=${REDIS_RUNDIR}

.include <bsd.port.pre.mk>

post-patch:
.if ${PORT_OPTIONS:MJEMALLOC}
	@${REINPLACE_CMD} '35s!Linux!FreeBSD!g' ${WRKSRC}/src/Makefile
.endif
.if ${PORT_OPTIONS:MLUA} || ${PORT_OPTIONS:MLUAJIT} || ${PORT_OPTIONS:MLUAJITOR}
	@cd ${WRKSRC}/deps/lua/src && ${CP} fpconv.* lua_* strbuf.* ${WRKSRC}/src/
.endif

post-build:
	${SED} ${SUB_LIST:S/$/!g/:S/^/ -e s!%%/:S/=/%%!/} \
		${WRKSRC}/redis.conf > ${WRKDIR}/redis.conf

do-install:
	${INSTALL_PROGRAM} ${BIN_FILES:C!^!${WRKSRC}/src/!} ${STAGEDIR}${PREFIX}/bin/
.if ${PORT_OPTIONS:MTRIB}
	${INSTALL_SCRIPT} ${WRKSRC}/src/redis-trib.rb ${STAGEDIR}${PREFIX}/bin/
.endif
	${INSTALL_DATA} ${WRKDIR}/redis.conf ${STAGEDIR}${PREFIX}/etc/redis.conf.sample
	${INSTALL_DATA} ${WRKSRC}/sentinel.conf ${STAGEDIR}${PREFIX}/etc/sentinel.conf.sample
	${MKDIR} ${STAGEDIR}${REDIS_LOGDIR} \
		${STAGEDIR}${REDIS_DBDIR} \
		${STAGEDIR}${REDIS_RUNDIR}

do-test:
	@cd ${WRKSRC} && ${TCLSH} tests/test_helper.tcl

.include <bsd.port.post.mk>
