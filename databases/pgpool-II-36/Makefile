PORTNAME=	pgpool-II
PORTVERSION=	3.6.28
CATEGORIES=	databases
MASTER_SITES=	http://www.pgpool.net/mediawiki/images/
PKGNAMESUFFIX=	36

MAINTAINER=	tz@FreeBSD.org
COMMENT=	Connection pool server for PostgreSQL

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/COPYING

USES=		gmake libtool pgsql:9.3+
USE_LDCONFIG=	yes
USE_RC_SUBR=	pgpool

GNU_CONFIGURE=	yes
PORTSCOUT=	limit:^3.6.[0-9]*

CONFLICTS=	pgpool-II

PORTDOCS=	*

OPTIONS_DEFINE=	DOCS SSL
OPTIONS_DEFAULT=	SSL

SSL_CONFIGURE_WITH=	openssl
SSL_USES=		ssl

post-install:
	@${MKDIR} ${STAGEDIR}/var/run/pgpool
	${INSTALL_LIB} ${WRKSRC}/src/libs/pcp/.libs/libpcp.so.1.0.0 ${STAGEDIR}${PREFIX}/lib

post-install-DOCS-on:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	cd ${WRKSRC} && ${COPYTREE_SHARE} doc ${STAGEDIR}${DOCSDIR} "-not -name Makefile.\*"
.for f in AUTHORS ChangeLog NEWS TODO
	${INSTALL_DATA} ${WRKSRC}/$f ${STAGEDIR}${DOCSDIR}
.endfor

.include <bsd.port.mk>
