PORTNAME=	jQuery-File-Upload
PORTVERSION=	0.30
PORTREVISION=	2
CATEGORIES=	www perl5
MASTER_SITES=	CPAN
PKGNAMEPREFIX=	p5-

MAINTAINER=	perl@FreeBSD.org
COMMENT=	Perl extension for jQuery File Upload plugin

RUN_DEPENDS=	\
	p5-Data-GUID>0:devel/p5-Data-GUID \
	p5-JSON>0:converters/p5-JSON \
	p5-JSON-XS>0:converters/p5-JSON-XS \
	p5-Net-SSH2>0:net/p5-Net-SSH2 \
	p5-URI>0:net/p5-URI
BUILD_DEPENDS=	${RUN_DEPENDS}

USES=		magick:6,run perl5
USE_PERL5=	configure
NO_ARCH=	YES

.include <bsd.port.mk>
