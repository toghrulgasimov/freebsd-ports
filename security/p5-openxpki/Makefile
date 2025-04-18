# Created by: Sergei Vyshenski <svysh.fbsd@gmail.com>

PORTNAME=	openxpki
DISTVERSIONPREFIX=	v
DISTVERSION=	3.16.1
CATEGORIES=	security perl5
PKGNAMEPREFIX=	p5-

MAINTAINER=	svysh.fbsd@gmail.com
COMMENT=	Perl based trustcenter for PKI: universal server building block

LICENSE=	APACHE20
LICENSE_FILE=	${WRKSRC}/LICENSE

MY_DEPENDS=	bash:shells/bash \
		p5-Archive-Zip>=0:archivers/p5-Archive-Zip \
		p5-Cache-LRU>=0:devel/p5-Cache-LRU \
		p5-CGI-Fast>=2.10:www/p5-CGI-Fast \
		p5-CGI-Session>=3.95:www/p5-CGI-Session \
		p5-CGI>=4.21:www/p5-CGI \
		p5-Class-Accessor-Chained>=0:devel/p5-Class-Accessor-Chained \
		p5-Class-Std>=0.0.8:devel/p5-Class-Std \
		p5-Config-GitLike>=0:devel/p5-Config-GitLike \
		p5-Config-Merge>=1:devel/p5-Config-Merge \
		p5-Config-Std>=0:devel/p5-Config-Std \
		p5-Connector>=1.43:devel/p5-Connector \
		p5-Crypt-Argon2>=0.007:security/p5-Crypt-Argon2 \
		p5-Crypt-CBC>=2.29:security/p5-Crypt-CBC \
		p5-Crypt-JWT>=0.032:security/p5-Crypt-JWT \
		p5-Crypt-LibSCEP>=0.6:security/p5-Crypt-LibSCEP \
		p5-Crypt-OpenSSL-AES>=0.02:security/p5-Crypt-OpenSSL-AES \
		p5-Crypt-PKCS10>=2.000:security/p5-Crypt-PKCS10 \
		p5-Crypt-Rijndael>=1.13:security/p5-Crypt-Rijndael \
		p5-Crypt-SMIME>=0:security/p5-Crypt-SMIME \
		p5-Crypt-SSLeay>=0:security/p5-Crypt-SSLeay \
		p5-Crypt-X509-CRL>=0.1:security/p5-Crypt-X509-CRL \
		p5-Crypt-X509>=0.53:security/p5-Crypt-X509 \
		p5-CryptX>=0.068:security/p5-CryptX \
		p5-Data-Password>=0:security/p5-Data-Password \
		p5-Data-Serializer>=0.44:devel/p5-Data-Serializer \
		p5-Data-UUID>=0:devel/p5-Data-UUID \
		p5-DateTime-Format-DateParse>=0.04:devel/p5-DateTime-Format-DateParse \
		p5-DBD-Mock>=1.45:databases/p5-DBD-Mock \
		p5-DBIx-Handler>=0.14:databases/p5-DBIx-Handler \
		p5-Devel-NYTProf>=0:devel/p5-Devel-NYTProf \
		p5-IO-Prompt>=0.099004:devel/p5-IO-Prompt \
		p5-IPC-ShareLite>=0:devel/p5-IPC-ShareLite \
		p5-JSON>=0:converters/p5-JSON \
		p5-Locale-libintl>=0:devel/p5-Locale-libintl \
		p5-Log-Log4perl-Layout-JSON>=0:devel/p5-Log-Log4perl-Layout-JSON \
		p5-LWP-Protocol-connect>=0:www/p5-LWP-Protocol-connect \
		p5-LWP-Protocol-https>=0:www/p5-LWP-Protocol-https \
		p5-Mail-RFC822-Address>=0:mail/p5-Mail-RFC822-Address \
		p5-Moose>=0:devel/p5-Moose \
		p5-MooseX-NonMoose>=0:devel/p5-MooseX-NonMoose \
		p5-MooseX-Params-Validate>=0.21:devel/p5-MooseX-Params-Validate \
		p5-Net-DNS>0.83:dns/p5-Net-DNS \
		p5-Net-IP>=0:net-mgmt/p5-Net-IP \
		p5-Net-Server>=0.94:net/p5-Net-Server \
		p5-NetAddr-IP>=0:net-mgmt/p5-NetAddr-IP \
		p5-openxpki-i18n>=2.0.3:security/p5-openxpki-i18n \
		p5-Path-Class>=0:devel/p5-Path-Class \
		p5-perl-ldap>=0.32:net/p5-perl-ldap \
		p5-Pod-POM>=2.01:textproc/p5-Pod-POM \
		p5-Proc-Daemon>=0.23:devel/p5-Proc-Daemon \
		p5-Proc-ProcessTable>=0.43:devel/p5-Proc-ProcessTable \
		p5-Proc-SafeExec>=1.4:devel/p5-Proc-SafeExec \
		p5-Regexp-Common>=2:textproc/p5-Regexp-Common \
		p5-RT-Client-REST>=0:www/p5-RT-Client-REST \
		p5-SOAP-Lite>=0:net/p5-SOAP-Lite \
		p5-SQL-Abstract-More>=1.28:databases/p5-SQL-Abstract-More \
		p5-Switch>=0:lang/p5-Switch \
		p5-Sys-SigAction>=0.06:devel/p5-Sys-SigAction \
		p5-Template-Toolkit>=2.15:www/p5-Template-Toolkit \
		p5-Text-CSV_XS>=0.23:textproc/p5-Text-CSV_XS \
		p5-TimeDate>=0:devel/p5-TimeDate \
		p5-Workflow>=0.31:devel/p5-Workflow \
		p5-XML-Filter-XInclude>=0:textproc/p5-XML-Filter-XInclude \
		p5-XML-SAX-Writer>=0:textproc/p5-XML-SAX-Writer \
		p5-XML-Validator-Schema>=0:textproc/p5-XML-Validator-Schema
BUILD_DEPENDS=	${MY_DEPENDS}
RUN_DEPENDS=	${MY_DEPENDS}
TEST_DEPENDS=	p5-DBD-SQLite>=1.52:databases/p5-DBD-SQLite \
		p5-Test-Pod-Coverage>=1.00:devel/p5-Test-Pod-Coverage \
		p5-Test-Pod>=1.00:devel/p5-Test-Pod \
		p5-Test-Prereq>=0:devel/p5-Test-Prereq

USES=		gmake perl5 shebangfix ssl
USE_GITHUB=	yes
GH_PROJECT=	openxpki-config:conf
GH_TAGNAME=	${DISTVERSIONPREFIX}${_conf_VERSION}:conf
_conf_VERSION=	3.16

USE_PERL5=	configure
USE_RC_SUBR=	openxpki
SHEBANG_FILES=	bin/*
SHEBANG_GLOB=	*.fcgi *.pl *.pm *.t*

NO_ARCH=	yes
# stay with stable versions only:
PORTSCOUT=	limitw:1,even
SUB_FILES=	pkg-message

WRKSRC_SUBDIR=	core/server/

USERS=		openxpki
GROUPS=		openxpki

PORTDOCS=	*
PORTEXAMPLES=	*
OPTIONS_DEFINE=	DOCS EXAMPLES GRAPHVIZ

GRAPHVIZ_DESC=		With graphical visualization of workflows?
GRAPHVIZ_RUN_DEPENDS=	dot:graphics/graphviz \
			imgsize:graphics/p5-Image-Size

post-extract:
	@${MV} ${WRKSRC_conf}/* ${WRKSRC}/../../config/

post-patch:
	@${REINPLACE_CMD} -e 's|..ENV{PERL} .vergen --format version.|"${PORTVERSION}"|g' ${WRKSRC}/Makefile.PL
	@${REINPLACE_CMD} -e 's|..vergen --format version.|"${PORTVERSION}"|g' ${WRKSRC}/Makefile.PL
	@( \
	cd ${WRKSRC}/../..; \
	${FIND} config core/server doc qatest tools -type f -print0 >filelist; \
	${CAT} filelist | ${XARGS} -0 -I % ${REINPLACE_CMD} -e 's|/etc/openxpki|${PREFIX}/etc/openxpki|g' "%"; \
	${CAT} filelist | ${XARGS} -0 -I % ${REINPLACE_CMD} -e 's|/var/run/openxpkid.pid|/var/openxpki/openxpkid.pid|g' "%"; \
	${CAT} filelist | ${XARGS} -0 -I % ${REINPLACE_CMD} -e 's|/var/openxpki/\([^\.]*\)\.log|/var/log/openxpki/\1\.log|g' "%"; \
	${CAT} filelist | ${XARGS} -0 -I % ${RM} "%.bak"; \
	${RM} filelist; \
	)
	@${MKDIR} ${WRKSRC}/t/var/log/openxpki

post-install:
	@${MKDIR} ${STAGEDIR}/var/openxpki/session
	@${MKDIR} ${STAGEDIR}/var/log/openxpki
	@${MKDIR} ${STAGEDIR}${PREFIX}/etc/openxpki

post-install-DOCS-on:
	${MKDIR} ${STAGEDIR}${DOCSDIR}
	(cd ${WRKSRC}/../../doc && ${COPYTREE_SHARE} . ${STAGEDIR}${DOCSDIR})

post-install-EXAMPLES-on:
	${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	(cd ${WRKSRC}/../.. && ${COPYTREE_SHARE} config ${STAGEDIR}${EXAMPLESDIR})
	(cd ${WRKSRC} && ${COPYTREE_SHARE} "htdocs cgi-bin" ${STAGEDIR}${EXAMPLESDIR})

.include <bsd.port.mk>
