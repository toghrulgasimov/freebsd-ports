PORTNAME=	netbox
DISTVERSIONPREFIX=	v
DISTVERSION=	3.0.12
PORTREVISION=	1
CATEGORIES=	net-mgmt python

MAINTAINER=	kai@FreeBSD.org
COMMENT=	IP address management tool

LICENSE=	APACHE20
LICENSE_FILE=	${WRKSRC}/LICENSE.txt

# NetBox has fixed Python package dependencies listed in "requirements.txt"
# which are not checked during build/runtime because they're usually installed
# via devel/py-pip.
#
# As a rule, slight deviations are usally not a problem, but there are a few
# Django packages that are known for regressions in conjunction with NetBox and
# should therefore only be updated with caution.
#
# - devel/py-dj32-django-rq
# - www/py-dj32-django-filter
# - www/py-dj32-django-tables2
# - www/py-dj32-djangorestframework (in conjunction with www/py-dj32-drf-yasg)
#
BUILD_DEPENDS=	${PYTHON_PKGNAMEPREFIX}markdown-include>=0.6.0<1:textproc/py-markdown-include@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}mkdocs-material>=7.3.6<9:textproc/py-mkdocs-material@${PY_FLAVOR}
RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}django32>=3.2.9<3.3:www/py-django32@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}dj32-django-cors-headers>=3.10.0<4:www/py-dj32-django-cors-headers@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}dj32-django-debug-toolbar>=3.2.2<4:www/py-dj32-django-debug-toolbar@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}dj32-django-filter>=21.1<22:www/py-dj32-django-filter@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}dj32-django-graphiql-debug-toolbar>=0.2.0<1:www/py-dj32-django-graphiql-debug-toolbar@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}dj32-django-mptt>=0.13.4<0.14:www/py-dj32-django-mptt@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}dj32-django-prometheus>=2.1.0<2.3:www/py-dj32-django-prometheus@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}dj32-django-redis>=5.0.0<6:www/py-dj32-django-redis@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}dj32-django-rq>=2.4.1<2.6:devel/py-dj32-django-rq@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}dj32-django-tables2>=2.4.1<2.5:www/py-dj32-django-tables2@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}dj32-django-taggit>=1.5.1<3:www/py-dj32-django-taggit@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}dj32-django-timezone-field>=4.1.2<5:www/py-dj32-django-timezone-field@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}dj32-djangorestframework>=3.12.4<3.13.0:www/py-dj32-djangorestframework@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}dj32-drf-yasg>=1.20.0<1.21:www/py-dj32-drf-yasg@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}dj32-graphene-django>=2.15.0<3:devel/py-dj32-graphene-django@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}django-pglocks>=1.0.4<1.1:www/py-django-pglocks@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}Jinja2>=3.0.1<4:devel/py-Jinja2@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}markdown>=3.3.4<3.5:textproc/py-markdown@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}netaddr>=0.8.0<1:net/py-netaddr@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}pillow>=8.2.0:graphics/py-pillow@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}psycopg2>=2.9.1<3:databases/py-psycopg2@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}svgwrite>=1.4.1<2:graphics/py-svgwrite@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}tablib>=3.1.0<3.2:textproc/py-tablib@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}yaml>=5.4.1<7:devel/py-yaml@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}gunicorn>=19.9.0<21:www/py-gunicorn@${PY_FLAVOR}

USES=		cpe pgsql:9.6+ python:3.7+
CPE_VENDOR=	netbox_project
USE_GITHUB=	yes
GH_ACCOUNT=	netbox-community

SUB_FILES=	850.netbox-housekeeping.sample netbox_rq.sample netboxrc.sample pkg-message
SUB_LIST=	DATADIR=${DATADIR} PYTHON_CMD=${PYTHON_CMD} PYTHON_VER=${PYTHON_VER} WWWOWN=${WWWOWN}
NO_ARCH=	yes

OPTIONS_DEFINE=	DOCS EXAMPLES

do-build:
	cd ${WRKSRC} && ${PYTHON_CMD} -m mkdocs build

do-install:
	cd ${WRKSRC}/netbox ; \
	for src in $$( ${FIND} . ! -name '*.bak' ) ; do \
		dst=${STAGEDIR}${DATADIR}$${src#.} ; \
		if ${TEST} -d "$$src" ; then \
			${MKDIR} "$$dst" ; \
		else \
			${INSTALL_DATA} "$$src" "$$dst" ; \
		fi \
	done

post-install-DOCS-on:
	cd ${WRKSRC}/docs ; \
	${MKDIR} ${STAGEDIR}${DOCSDIR} ; \
	for src in $$( ${FIND} . ! -name '*.bak' ) ; do \
		dst=${STAGEDIR}${DOCSDIR}$${src#.} ; \
		if ${TEST} -d "$$src" ; then \
			${MKDIR} "$$dst" ; \
		else \
			${INSTALL_DATA} "$$src" "$$dst" ; \
		fi \
	done

post-install-EXAMPLES-on:
	@${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKDIR}/850.netbox-housekeeping.sample ${STAGEDIR}${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKDIR}/netbox_rq.sample ${STAGEDIR}${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKDIR}/netboxrc.sample ${STAGEDIR}${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/contrib/apache.conf ${STAGEDIR}${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/contrib/gunicorn.py ${STAGEDIR}${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/contrib/nginx.conf ${STAGEDIR}${EXAMPLESDIR}

.include <bsd.port.mk>
