# Created by: Po-Chuan Hsieh <sunpoet@FreeBSD.org>

PORTNAME=	Log-ger
PORTVERSION=	0.038
CATEGORIES=	devel perl5
MASTER_SITES=	CPAN
PKGNAMEPREFIX=	p5-

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	Lightweight, flexible logging framework

LICENSE=	ART10 GPLv1+
LICENSE_COMB=	dual
LICENSE_FILE=	${WRKSRC}/LICENSE

BUILD_DEPENDS=	${RUN_DEPENDS}
RUN_DEPENDS=	p5-Data-Dmp>=0.240:devel/p5-Data-Dmp \
		p5-Sub-Name>=0,1:devel/p5-Sub-Name

USES=		perl5
USE_PERL5=	configure

NO_ARCH=	yes

.include <bsd.port.mk>
