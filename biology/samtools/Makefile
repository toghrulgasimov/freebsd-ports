# Created by: Reed A. Cartwright <cartwright@asu.edu>

PORTNAME=	samtools
DISTVERSION=	1.14
CATEGORIES=	biology

MAINTAINER=	jwb@FreeBSD.org
COMMENT=	Tools for manipulating next-generation sequencing data

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE

LIB_DEPENDS=	libhts.so:biology/htslib
TEST_DEPENDS=	bash:shells/bash

USES=		autoreconf gmake localbase ncurses perl5 python:env shebangfix

USE_GITHUB=	yes

USE_PERL5=	test
GNU_CONFIGURE=	yes
SHEBANG_FILES=	misc/*.pl misc/plot-bamstats test/test.pl

TEST_TARGET=	test

.include <bsd.port.mk>
