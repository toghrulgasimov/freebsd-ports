PORTNAME=	flexget
DISTVERSIONPREFIX=	v
PORTVERSION=	3.2.8
CATEGORIES=	www

MAINTAINER=	jbeich@FreeBSD.org
COMMENT=	Multipurpose automation tool for all of your media

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE

RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}sqlalchemy13>=1.3.10:databases/py-sqlalchemy13@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}Jinja2>=3.0:devel/py-Jinja2@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}rebulk>=2.0.0:devel/py-rebulk@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}rpyc>=5.0:devel/py-RPyC@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}apscheduler>=3.2.0:devel/py-apscheduler@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}dateutil>0:devel/py-dateutil@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}jsonschema>=2.0:devel/py-jsonschema@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}loguru>=0.4.1:devel/py-loguru@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}more-itertools>0:devel/py-more-itertools@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}pyparsing>=2.4.7:devel/py-pyparsing@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}yaml>=4.2:devel/py-yaml@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}guessit>=3.2.0:multimedia/py-guessit@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}pynzb>0:news/py-pynzb@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}zxcvbn>0:security/py-zxcvbn@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}plumbum>=1.2:sysutils/py-plumbum@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}psutil>=5.8.0:sysutils/py-psutil@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}feedparser>=6.0.2:textproc/py-feedparser@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}rich>=9.0.0:textproc/py-rich@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}rss2gen>0:textproc/py-rss2gen@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}beautifulsoup>=4.5:www/py-beautifulsoup@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}cherrypy>=3.7.0:www/py-cherrypy@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}Flask>=0.7:www/py-flask@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}Flask-Compress>=1.2.1:www/py-flask-compress@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}Flask-Cors>=2.1.2:www/py-flask-cors@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}Flask-Login>=0.4.0:www/py-flask-login@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}Flask-RESTful>=0.3.3:www/py-flask-restful@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}flask-restx>=0.5.1:www/py-flask-restx@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}html5lib>=0.11:www/py-html5lib@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}requests>=2.20.0:www/py-requests@${PY_FLAVOR}
TEST_DEPENDS=	${PYTHON_PKGNAMEPREFIX}pytest>=3.3:devel/py-pytest@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}vcrpy>0:devel/py-vcrpy@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}boto3>0:www/py-boto3@${PY_FLAVOR}

USES=		python:3.6+
USE_GITHUB=	yes
USE_PYTHON=	autoplist distutils
GH_PROJECT=	Flexget
NO_ARCH=	yes

post-extract:
# Unlock dependencies' versions
	@${MV} ${WRKSRC}/requirements.in ${WRKSRC}/requirements.txt

do-test:
	@(cd ${TEST_WRKSRC} && ${SETENV} ${TEST_ENV} ${PYTHON_CMD} -m pytest)

.include <bsd.port.mk>
