# Created by: Autrijus Tang <autrijus@autrijus.org>

PORTNAME=	Module-Signature
PORTVERSION=	0.88
CATEGORIES=	security perl5
MASTER_SITES=	CPAN
PKGNAMEPREFIX=	p5-

MAINTAINER=	perl@FreeBSD.org
COMMENT=	Module signature file manipulation

LICENSE=	CC0-1.0

BUILD_DEPENDS=	${RUN_DEPENDS}
RUN_DEPENDS=	p5-PAR-Dist>=0:devel/p5-PAR-Dist
TEST_DEPENDS=	p5-IPC-Run>=0:devel/p5-IPC-Run

USES=		perl5
USE_PERL5=	configure

CONFIGURE_ENV=	PERL_MM_USE_DEFAULT="yes"
NO_ARCH=	yes

OPTIONS_MULTI=	GPG
OPTIONS_MULTI_GPG=	GPG1 GPG2
OPTIONS_DEFAULT=GPG2

GPG1_DESC=	Use GnuPG version 1
GPG2_DESC=	Use GnuPG version 2

GPG1_RUN_DEPENDS=	gpgv:security/gnupg1
GPG2_RUN_DEPENDS=	gpgv2:security/gnupg

.include <bsd.port.mk>
