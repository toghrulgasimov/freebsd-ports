# Created by: cy@FreeBSD.org

PORTNAME=	cfengine-masterfiles
PORTVERSION=	3.${CFENGINE_COMMIT_DATE}
CATEGORIES=	sysutils
PKGNAMESUFFIX=	-devel
HASH=		251b798d
CFENGINE_COMMIT_DATE=	2021.12.28

MAINTAINER=	cy@FreeBSD.org
#		gjb@FreeBSD.org is also committer for this port
#		skreuzer@FreeBSD.org is also committer for this port
COMMENT=	cfengine sample policies for installations and upgrades

LICENSE=	GPLv3

USE_GITHUB=	yes
GH_ACCOUNT=	cfengine
GH_PROJECT=	masterfiles
GH_TAGNAME=	${HASH}
CPE_VENDOR=	gnu
CPE_PRODUCT=	cfengine

CONFLICTS=	cfengine-masterfiles3[0-9]-* cfengine-masterfiles31[02-9]-* \
		cfengine-masterfiles-3.*

RUN_DEPENDS=	cf-agent:sysutils/cfengine${PKGNAMESUFFIX}

FETCH_BEFORE_ARGS=	-o ${DISTDIR}/${DISTFILES}

MAKE_JOBS_UNSAFE=	yes
USES=		autoreconf:build cpe gmake python:build
HAS_CONFIGURE=	yes
EXAMPLESDIR=	${PREFIX}/share/examples/cfengine-masterfiles
CONFIGURE_SCRIPT=	./autogen.sh
CONFIGURE_ARGS=	--prefix=${EXAMPLESDIR}
CONFIGURE_ENV=	EXPLICIT_VERSION=${PORTVERSION}-${HASH}

.include <bsd.port.mk>
