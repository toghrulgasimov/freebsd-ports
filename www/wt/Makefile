# Created by: Mohammad S. Babaei <info@babaei.net>

PORTNAME=	wt
DISTVERSION=	4.6.1
CATEGORIES=	www

MAINTAINER=	info@babaei.net
COMMENT=	Widget-centric C++ library for developing web applications

LICENSE=	GPLv2
LICENSE_FILE=	${WRKSRC}/LICENSE

LIB_DEPENDS=	libpng.so:graphics/png \
		libboost_system.so:devel/boost-libs \
		libGraphicsMagick.so:graphics/GraphicsMagick

USES=		cmake compiler:c++14-lang cpe pkgconfig ssl
USE_GITHUB=	yes
GH_ACCOUNT=	emweb
CPE_VENDOR=	emweb
USE_XORG=	x11
USE_LDCONFIG=	yes

CMAKE_ARGS=	-DCONFIGDIR:STRING=${LOCALBASE}/etc/${PORTNAME} \
		-DGM_PREFIX:STRING=${LOCALBASE} \
		-DEXAMPLES_DESTINATION:STRING=share/examples/${PORTNAME} \
		-DSSL_PREFIX:STRING=/usr \
		-DZLIB_PREFIX:STRING=/usr \
		-DCONNECTOR_ISAPI:BOOL=OFF \
		-DWEBUSER:STRING=www \
		-DWEBGROUP:STRING=www \
		-DWT_WRASTERIMAGE_IMPLEMENTATION:STRING=GraphicsMagick \
		-DENABLE_SSL:BOOL=ON \
		-DDESTDIR:STRING=${STAGEDIR}

OPTIONS_DEFINE=	\
	EXAMPLES \
	TESTS \
	RESOURCES \
	HARU \
	PANGO \
	QT5 \
	OPENGL \
	SAML \
	LIBWTTEST \
	UNWIND
OPTIONS_DEFAULT=	\
	TESTS \
	RESOURCES \
	HARU \
	PANGO \
	OPENGL \
	LIBWTTEST
OPTIONS_GROUP=	CONNECTOR DBO WSTRING
OPTIONS_SUB=	yes
NO_OPTIONS_SORT=	yes

EXAMPLES_DESC=		Install examples (implies SQLITE3 and WTHTTP)
TESTS_DESC=		Build Wt tests
RESOURCES_DESC=		Install resources directory
HARU_DESC=		Enable Haru Free PDF Library
SAML_DESC=		Build built-in SAML service provider for Wt::Auth
LIBWTTEST_DESC=		Build Wt::Test for automated (integration/unit) tests
UNWIND_DESC=		Build Wt with stacktrace support using libunwind

OPTIONS_GROUP_CONNECTOR=	FCGI WTHTTP
OPTIONS_DEFAULT+=	FCGI WTHTTP
CONNECTOR_DESC=		Connector
FCGI_DESC=		Build FastCGI connector
WTHTTP_DESC=		Build Wt stand-alone httpd connector

OPTIONS_GROUP_DBO=	SQLITE3 POSTGRES FIREBIRD MYSQL
OPTIONS_DEFAULT+=	SQLITE3
DBO_DESC=		Wt::DBO
SQLITE3_DESC=		Build Wt with SQLite 3 support
POSTGRES_DESC=		Build Wt with PostgreSQL support
FIREBIRD_DESC=		Build Wt with FirebirdSQL support
MYSQL_DESC=		Build Wt with MariaDB or MySQL support

EXAMPLES_IMPLIES=	SQLITE3 WTHTTP
EXAMPLES_CMAKE_BOOL=	BUILD_EXAMPLES INSTALL_EXAMPLES

FCGI_CMAKE_BOOL=	CONNECTOR_FCGI
FCGI_LIB_DEPENDS=	libfcgi.so:www/fcgi \
			libfcgi++.so:www/fcgi
FCGI_CMAKE_ON=		-DFCGI_PREFIX:STRING=${LOCALBASE}

FIREBIRD_CMAKE_BOOL=	ENABLE_FIREBIRD
FIREBIRD_USES=		firebird

HARU_CMAKE_BOOL=	ENABLE_HARU
HARU_LIB_DEPENDS=	libhpdf.so:print/libharu
HARU_CMAKE_ON=	-DHARU_PREFIX:STRING=${LOCALBASE}

LIBWTTEST_CMAKE_BOOL=	ENABLE_LIBWTTEST

MYSQL_USES=		mysql
MYSQL_CMAKE_BOOL=	ENABLE_MYSQL
MYSQL_CMAKE_ON=		-DMYSQL_PREFIX:STRING=${LOCALBASE} \
			-DENABLE_LIBWTDBO:BOOL=ON

OPENGL_CMAKE_BOOL=	ENABLE_OPENGL
OPENGL_USES=            gl xorg
OPENGL_USE=             GL=gl,glew xorg=x11

PANGO_CMAKE_BOOL=	ENABLE_PANGO
PANGO_USES=		gnome
PANGO_USE=              GNOME=pango
PANGO_LIB_DEPENDS=	libfontconfig.so:x11-fonts/fontconfig

POSTGRES_CMAKE_BOOL=	ENABLE_POSTGRES
POSTGRES_USES=		pgsql
POSTGRES_CMAKE_ON=	-DPOSTGRES_PREFIX:STRING=${LOCALBASE} \
			-DENABLE_LIBWTDBO:BOOL=ON

QT5_CMAKE_BOOL=		ENABLE_QT5
QT5_USES=		qt:5
QT5_USE=                qt=buildtools_build,core

RESOURCES_CMAKE_BOOL=	INSTALL_RESOURCES

SAML_CMAKE_BOOL=	ENABLE_SAML
SAML_LIB_DEPENDS=	libsaml.so:security/opensaml \
			liblog4shib.so:devel/log4shib \
			libxerces-c-3.2.so:textproc/xerces-c3 \
			libxml-security-c.so:security/apache-xml-security-c \
			libxmltooling.so:devel/xmltooling

SQLITE3_CMAKE_BOOL=	ENABLE_SQLITE
SQLITE3_USES=		sqlite:3
SQLITE3_CMAKE_ON=	-DENABLE_LIBWTDBO:BOOL=ON

TESTS_CMAKE_BOOL=	BUILD_TESTS

UNWIND_CMAKE_BOOL=	ENABLE_UNWIND
UNWIND_LIB_DEPENDS=	libunwind.so:devel/libunwind

WTHTTP_CMAKE_BOOL=	CONNECTOR_HTTP

PORTEXAMPLES=	*

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MSQLITE3} || \
    ${PORT_OPTIONS:MPOSTGRES} || \
    ${PORT_OPTIONS:MMYSQL}
PLIST_SUB+=	DBO=""
.else
PLIST_SUB+=	DBO="@comment "
.endif

post-install:
	@${RM} ${STAGEDIR}${ETCDIR}/wt_config.xml
	@${MKDIR} ${STAGEDIR}${ETCDIR}
	${INSTALL_DATA} ${BUILD_WRKSRC}/wt_config.xml \
		${STAGEDIR}${ETCDIR}/wt_config.xml.sample

.include <bsd.port.mk>
