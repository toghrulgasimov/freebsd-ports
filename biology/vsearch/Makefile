PORTNAME=		vsearch
DISTVERSIONPREFIX=	v
DISTVERSION=		2.19.0
CATEGORIES=		biology

MAINTAINER=	jwb@FreeBSD.org
COMMENT=	Versatile open-source tool for metagenomics

LICENSE=	GPLv3
LICENSE_FILE=	${WRKSRC}/LICENSE.txt

ONLY_FOR_ARCHS=		aarch64 amd64 powerpc64le
ONLY_FOR_ARCHS_REASON=	Explicitly enumerated by upstream developers

LIB_DEPENDS=	libsysinfo.so:devel/libsysinfo

USES=		autoreconf ghostscript:build gmake localbase
USE_GITHUB=	yes

GH_ACCOUNT=	torognes
GNU_CONFIGURE=	yes

PLIST_FILES=	bin/vsearch man/man1/vsearch.1.gz
PORTDOCS=	*

OPTIONS_DEFINE=	DOCS
OPTIONS_SUB=	yes

.include <bsd.port.mk>
