# Created by: Michael Ranner <michael@ranner.eu>

PORTNAME=	pdfgrep
PORTVERSION=	2.1.1
PORTREVISION=	35
CATEGORIES=	textproc
MASTER_SITES=	https://pdfgrep.org/download/

MAINTAINER=	michael@ranner.eu
COMMENT=	Tool to search text in PDF files

LICENSE=	GPLv2+
LICENSE_FILE=	${WRKSRC}/COPYING

LIB_DEPENDS=	libgcrypt.so:security/libgcrypt \
		libpoppler.so:graphics/poppler \
		libgpg-error.so:security/libgpg-error

GNU_CONFIGURE=	yes
USES=		compiler:c11 pkgconfig

PLIST_FILES=	bin/pdfgrep man/man1/pdfgrep.1.gz \
		share/bash-completion/completions/pdfgrep \
		share/zsh/site-functions/_pdfgrep

OPTIONS_DEFINE=		LIBPCRE
LIBPCRE_DESC=		Enable Perl compatable expressions
LIBPCRE_LIB_DEPENDS=	libpcre.so:devel/pcre
LIBPCRE_CONFIGURE_WITH=	libpcre

.include <bsd.port.mk>
