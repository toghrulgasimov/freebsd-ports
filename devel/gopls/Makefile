PORTNAME=	gopls
DISTVERSIONPREFIX=	v
DISTVERSION=	0.7.4
CATEGORIES=	devel

MAINTAINER=	fuz@fuz.su
COMMENT=	Go language LSP server

LICENSE=	BSD3CLAUSE
LICENSE_FILE=	${WRKSRC}/LICENSE

USES=		go:modules
GO_MODULE=	golang.org/x/tools/gopls
GO_TARGET=	.

OPTIONS_DEFINE=	DOCS

post-install-DOCS-on:
	${MKDIR} ${STAGEDIR}${DOCSDIR}
	cd ${WRKSRC} && ${COPYTREE_SHARE} "README.md doc" ${STAGEDIR}${DOCSDIR}
	${RM} ${STAGEDIR}${DOCSDIR}/doc/*.go

.include <bsd.port.mk>
