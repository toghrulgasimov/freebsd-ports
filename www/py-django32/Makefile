# Created by: Jose Alonso Cardenas Marquez <acardenas@bsd.org.pe>

PORTNAME=	django
PORTVERSION=	3.2.11
CATEGORIES=	www python
MASTER_SITES=	CHEESESHOP \
		https://www.djangoproject.com/m/releases/${PORTVERSION}/
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}
PKGNAMESUFFIX=	32
DISTNAME=	Django-${PORTVERSION}
DIST_SUBDIR=	python

MAINTAINER=	python@FreeBSD.org
COMMENT=	High-level Python Web Framework

LICENSE=	BSD3CLAUSE
LICENSE_FILE=	${WRKSRC}/LICENSE

RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}pytz>0:devel/py-pytz@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}asgiref>0:www/py-asgiref@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}sqlparse>=0:databases/py-sqlparse@${PY_FLAVOR}
TEST_DEPENDS=	${PYTHON_PKGNAMEPREFIX}tblib>0:devel/py-tblib@${PY_FLAVOR}

USES=		cpe python:3.6+ shebangfix
USE_PYTHON=	autoplist distutils

NO_ARCH=	yes

DOCSDIR=	${PREFIX}/share/doc/py-django
PLIST_FILES=	man/man1/django-admin.1.gz
PORTDOCS=	*

SHEBANG_FILES=	django/bin/django-admin.py \
		django/conf/project_template/manage.py-tpl

CONFLICTS_INSTALL=	${PYTHON_PKGNAMEPREFIX}django22 \
			${PYTHON_PKGNAMEPREFIX}django31

CPE_VENDOR=	djangoproject

# Upstream archive contains files with UTF-8 names
EXTRACT_CMD=	${SETENV} LC_ALL=en_US.UTF-8 /usr/bin/bsdtar

OPTIONS_DEFINE=	DOCS HTMLDOCS
OPTIONS_GROUP=	DATABASE
OPTIONS_GROUP_DATABASE=	PGSQL MYSQL SQLITE
OPTIONS_DEFAULT=SQLITE
HTMLDOCS_DESC=	Install HTML documentation (requires Sphinx)

HTMLDOCS_BUILD_DEPENDS=	${PYTHON_PKGNAMEPREFIX}sphinx>=0,1:textproc/py-sphinx@${PY_FLAVOR}
HTMLDOCS_IMPLIES=	DOCS
PGSQL_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}psycopg2>0:databases/py-psycopg2@${PY_FLAVOR}
MYSQL_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}mysqlclient>=1.3.13:databases/py-mysqlclient@${PY_FLAVOR}
SQLITE_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}sqlite3>0:databases/py-sqlite3@${PY_FLAVOR}

post-build-HTMLDOCS-on:
	cd ${WRKSRC}/docs && ${MAKE} html SPHINXBUILD=sphinx-build-${PYTHON_VER}

post-install:
	${INSTALL_MAN} ${WRKSRC}/docs/man/* ${STAGEDIR}/${MAN1PREFIX}/man/man1
	@${ECHO_MSG}	""
	@${ECHO_MSG}	"	* See http://docs.djangoproject.com/ for complete documentation"
	@${ECHO_MSG}	""

post-install-HTMLDOCS-on:
	${MKDIR} ${STAGEDIR}/${DOCSDIR}
	${CP} -R ${WRKSRC}/docs/_build/html ${STAGEDIR}/${DOCSDIR}

do-test:
	@cd ${WRKSRC} && ${PYTHON_CMD} tests/runtests.py --settings=test_sqlite

.include <bsd.port.mk>
