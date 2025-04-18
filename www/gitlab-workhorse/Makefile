# Created by: Torsten Zuehlsdorff <tz@FreeBSD.org>

PORTNAME=	gitlab-workhorse
PORTVERSION=	14.6.0
PORTREVISION=	0
CATEGORIES=	www

MAINTAINER=	mfechner@FreeBSD.org
COMMENT=	Smart reverse proxy for GitLab

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/../LICENSE

BUILD_DEPENDS=	git>=2.16.2:devel/git
RUN_DEPENDS=	p5-Image-ExifTool>=0:graphics/p5-Image-ExifTool

USES=		gmake go:modules,no_targets
MAKE_ENV=	GOFLAGS="${GO_BUILDFLAGS}"
MAKE_ENV+=	${GO_ENV}
WRKSRC_SUBDIR=	workhorse

USE_GITLAB=	yes
GL_ACCOUNT=	gitlab-org
GL_PROJECT=	gitlab-foss
# Find the commit hash here: https://gitlab.com/gitlab-org/gitlab-foss/-/tags
GL_COMMIT=	3bc07a0be9ce3b8f736890a0513283f04796b37e

# for go dependencies
USE_GITHUB=	nodefault
# generated with: make gomod-vendor
# 105dd
GH_TUPLE=	\
		Azure:azure-pipeline-go:v0.2.3:azure_azure_pipeline_go/vendor/github.com/Azure/azure-pipeline-go \
		Azure:azure-storage-blob-go:v0.13.0:azure_azure_storage_blob_go/vendor/github.com/Azure/azure-storage-blob-go \
		Azure:go-autorest:79a63e70c4d8:azure_go_autorest_adal \
		Azure:go-autorest:autorest/v0.11.18:azure_go_autorest_autorest \
		Azure:go-autorest:b3a0b30a7423:azure_go_autorest_date \
		Azure:go-autorest:logger/v0.2.1:azure_go_autorest_logger \
		Azure:go-autorest:tracing/v0.6.0:azure_go_autorest_tracing \
		Azure:go-autorest:v14.2.0:azure_go_autorest/vendor/github.com/Azure/go-autorest \
		BurntSushi:toml:v0.3.1:burntsushi_toml/vendor/github.com/BurntSushi/toml \
		DataDog:datadog-go:v4.4.0:datadog_datadog_go/vendor/github.com/DataDog/datadog-go \
		DataDog:dd-trace-go:v1.31.1:datadog_dd_trace_go/vendor/gopkg.in/DataDog/dd-trace-go.v1 \
		DataDog:sketches-go:v1.0.0:datadog_sketches_go/vendor/github.com/DataDog/sketches-go \
		FZambia:sentinel:v1.0.0:fzambia_sentinel/vendor/github.com/FZambia/sentinel \
		Microsoft:go-winio:v0.4.19:microsoft_go_winio/vendor/github.com/Microsoft/go-winio \
		StackExchange:wmi:cbe66965904d:stackexchange_wmi/vendor/github.com/StackExchange/wmi \
		alecthomas:chroma:v0.7.3:alecthomas_chroma/vendor/github.com/alecthomas/chroma \
		aws:aws-sdk-go:v1.38.35:aws_aws_sdk_go/vendor/github.com/aws/aws-sdk-go \
		beorn7:perks:v1.0.1:beorn7_perks/vendor/github.com/beorn7/perks \
		census-ecosystem:opencensus-go-exporter-stackdriver:v0.13.8:census_ecosystem_opencensus_go_exporter_stackdriver/vendor/contrib.go.opencensus.io/exporter/stackdriver \
		census-instrumentation:opencensus-go:v0.23.0:census_instrumentation_opencensus_go/vendor/go.opencensus.io \
		census-instrumentation:opencensus-proto:v0.3.0:census_instrumentation_opencensus_proto/vendor/github.com/census-instrumentation/opencensus-proto \
		certifi:gocertifi:2c3bb06c6054:certifi_gocertifi/vendor/github.com/certifi/gocertifi \
		cespare:xxhash:v2.1.1:cespare_xxhash_v2/vendor/github.com/cespare/xxhash/v2 \
		client9:reopen:v1.0.0:client9_reopen/vendor/github.com/client9/reopen \
		danwakefield:fnmatch:cbb64ac3d964:danwakefield_fnmatch/vendor/github.com/danwakefield/fnmatch \
		davecgh:go-spew:v1.1.1:davecgh_go_spew/vendor/github.com/davecgh/go-spew \
		disintegration:imaging:v1.6.2:disintegration_imaging/vendor/github.com/disintegration/imaging \
		dlclark:regexp2:v1.2.0:dlclark_regexp2/vendor/github.com/dlclark/regexp2 \
		dominikh:go-tools:v0.1.3:dominikh_go_tools/vendor/honnef.co/go/tools \
		form3tech-oss:jwt-go:v3.2.2:form3tech_oss_jwt_go/vendor/github.com/form3tech-oss/jwt-go \
		getsentry:raven-go:v0.2.0:getsentry_raven_go/vendor/github.com/getsentry/raven-go \
		go-ole:go-ole:v1.2.4:go_ole_go_ole/vendor/github.com/go-ole/go-ole \
		go-yaml:yaml:9f266ea9e77c:go_yaml_yaml/vendor/gopkg.in/yaml.v3 \
		gogo:protobuf:v1.3.2:gogo_protobuf/vendor/github.com/gogo/protobuf \
		golang-jwt:jwt:v4.0.0:golang_jwt_jwt_v4/vendor/github.com/golang-jwt/jwt/v4 \
		golang:appengine:v1.6.7:golang_appengine/vendor/google.golang.org/appengine \
		golang:crypto:38f3c27a63bf:golang_crypto/vendor/golang.org/x/crypto \
		golang:gddo:af0f2af80721:golang_gddo/vendor/github.com/golang/gddo \
		golang:groupcache:41bb18bfe9da:golang_groupcache/vendor/github.com/golang/groupcache \
		golang:image:e7c1f5e7dbb8:golang_image/vendor/golang.org/x/image \
		golang:lint:83fdc39ff7b5:golang_lint/vendor/golang.org/x/lint \
		golang:mod:v0.4.2:golang_mod/vendor/golang.org/x/mod \
		golang:net:0714010a04ed:golang_net/vendor/golang.org/x/net \
		golang:oauth2:81ed05c6b58c:golang_oauth2/vendor/golang.org/x/oauth2 \
		golang:protobuf:v1.5.2:golang_protobuf/vendor/github.com/golang/protobuf \
		golang:sync:036812b2e83c:golang_sync/vendor/golang.org/x/sync \
		golang:sys:0981d6026fa6:golang_sys/vendor/golang.org/x/sys \
		golang:text:v0.3.6:golang_text/vendor/golang.org/x/text \
		golang:time:f8bda1e9f3ba:golang_time/vendor/golang.org/x/time \
		golang:tools:v0.1.0:golang_tools/vendor/golang.org/x/tools \
		golang:xerrors:5ec99f83aff1:golang_xerrors/vendor/golang.org/x/xerrors \
		gomodule:redigo:v2.0.0:gomodule_redigo/vendor/github.com/gomodule/redigo \
		google:go-cloud:v0.23.0:google_go_cloud/vendor/gocloud.dev \
		google:go-cmp:v0.5.5:google_go_cmp/vendor/github.com/google/go-cmp \
		google:go-genproto:4a47615972c2:google_go_genproto/vendor/google.golang.org/genproto \
		google:pprof:cbba55b83ad5:google_pprof/vendor/github.com/google/pprof \
		google:uuid:v1.2.0:google_uuid/vendor/github.com/google/uuid \
		google:wire:v0.5.0:google_wire/vendor/github.com/google/wire \
		googleapis:gax-go:v2.0.5:googleapis_gax_go_v2/vendor/github.com/googleapis/gax-go \
		googleapis:google-api-go-client:v0.46.0:googleapis_google_api_go_client/vendor/google.golang.org/api \
		googleapis:google-cloud-go:v0.81.0:googleapis_google_cloud_go/vendor/cloud.google.com/go \
		gopherjs:gopherjs:0766667cb4d1:gopherjs_gopherjs/vendor/github.com/gopherjs/gopherjs \
		gorilla:websocket:v1.4.1:gorilla_websocket/vendor/github.com/gorilla/websocket \
		grpc-ecosystem:go-grpc-middleware:v1.3.0:grpc_ecosystem_go_grpc_middleware/vendor/github.com/grpc-ecosystem/go-grpc-middleware \
		grpc-ecosystem:go-grpc-prometheus:v1.2.0:grpc_ecosystem_go_grpc_prometheus/vendor/github.com/grpc-ecosystem/go-grpc-prometheus \
		grpc:grpc-go:v1.38.0:grpc_grpc_go/vendor/google.golang.org/grpc \
		hashicorp:yamux:a95892c5f864:hashicorp_yamux/vendor/github.com/hashicorp/yamux \
		jmespath:go-jmespath:v0.4.0:jmespath_go_jmespath/vendor/github.com/jmespath/go-jmespath \
		johannesboyne:gofakes3:02d71f533bec:johannesboyne_gofakes3/vendor/github.com/johannesboyne/gofakes3 \
		jpillora:backoff:v1.0.0:jpillora_backoff/vendor/github.com/jpillora/backoff \
		jtolds:gls:v4.20.0:jtolds_gls/vendor/github.com/jtolds/gls \
		lightstep:lightstep-tracer-common:a8dfcb80d3a7:lightstep_lightstep_tracer_common_gogo/vendor/github.com/lightstep/lightstep-tracer-common \
		lightstep:lightstep-tracer-go:v0.24.0:lightstep_lightstep_tracer_go/vendor/github.com/lightstep/lightstep-tracer-go \
		mattn:go-ieproxy:v0.0.1:mattn_go_ieproxy/vendor/github.com/mattn/go-ieproxy \
		matttproud:golang_protobuf_extensions:v1.0.1:matttproud_golang_protobuf_extensions/vendor/github.com/matttproud/golang_protobuf_extensions \
		mitchellh:copystructure:v1.0.0:mitchellh_copystructure/vendor/github.com/mitchellh/copystructure \
		mitchellh:reflectwalk:v1.0.0:mitchellh_reflectwalk/vendor/github.com/mitchellh/reflectwalk \
		oklog:ulid:v2.0.2:oklog_ulid_v2/vendor/github.com/oklog/ulid/v2 \
		opentracing:opentracing-go:v1.2.0:opentracing_opentracing_go/vendor/github.com/opentracing/opentracing-go \
		philhofer:fwd:v1.0.0:philhofer_fwd/vendor/github.com/philhofer/fwd \
		pkg:errors:v0.9.1:pkg_errors/vendor/github.com/pkg/errors \
		pmezard:go-difflib:v1.0.0:pmezard_go_difflib/vendor/github.com/pmezard/go-difflib \
		prometheus:client_golang:v1.10.0:prometheus_client_golang/vendor/github.com/prometheus/client_golang \
		prometheus:client_model:v0.2.0:prometheus_client_model/vendor/github.com/prometheus/client_model \
		prometheus:common:v0.18.0:prometheus_common/vendor/github.com/prometheus/common \
		prometheus:procfs:v0.6.0:prometheus_procfs/vendor/github.com/prometheus/procfs \
		protocolbuffers:protobuf-go:v1.26.0:protocolbuffers_protobuf_go/vendor/google.golang.org/protobuf \
		rafaeljusto:redigomock:257e089e14a1:rafaeljusto_redigomock/vendor/github.com/rafaeljusto/redigomock \
		ryszard:goskiplist:2dfbae5fcf46:ryszard_goskiplist/vendor/github.com/ryszard/goskiplist \
		sebest:xff:671bd2870b3a:sebest_xff/vendor/github.com/sebest/xff \
		shabbyrobe:gocovmerge:3e036491d500:shabbyrobe_gocovmerge/vendor/github.com/shabbyrobe/gocovmerge \
		shirou:gopsutil:v2.20.1:shirou_gopsutil/vendor/github.com/shirou/gopsutil \
		sirupsen:logrus:v1.8.1:sirupsen_logrus/vendor/github.com/sirupsen/logrus \
		smartystreets:assertions:b2de0cb4f26d:smartystreets_assertions/vendor/github.com/smartystreets/assertions \
		smartystreets:goconvey:v1.6.4:smartystreets_goconvey/vendor/github.com/smartystreets/goconvey \
		stretchr:testify:v1.7.0:stretchr_testify/vendor/github.com/stretchr/testify \
		tinylib:msgp:v1.1.2:tinylib_msgp/vendor/github.com/tinylib/msgp \
		uber-go:atomic:v1.7.0:uber_go_atomic/vendor/go.uber.org/atomic \
		uber:jaeger-client-go:v2.27.0:uber_jaeger_client_go/vendor/github.com/uber/jaeger-client-go \
		uber:jaeger-lib:v2.4.1:uber_jaeger_lib/vendor/github.com/uber/jaeger-lib

GL_TUPLE=	gitlab-org:gitaly:df7dadcc3f74276a7176234d4b1475299f46c05c:gitlab_org_gitaly_v14/vendor/gitlab.com/gitlab-org/gitaly/v14 \
		gitlab-org:golang-archive-zip:84007c99e03b62ee4dc62a94048d6e59552299d7:gitlab_org_golang_archive_zip/vendor/gitlab.com/gitlab-org/golang-archive-zip \
		gitlab-org:labkit:9205b46eea68f47a36cefa783a306476f0b2dbfd:gitlab_org_labkit/vendor/gitlab.com/gitlab-org/labkit

PLIST_FILES=	bin/gitlab-resize-image \
		bin/gitlab-workhorse \
		bin/gitlab-zip-cat \
		bin/gitlab-zip-metadata
PLIST_DIRS=	${WWWDIR}

# 11dd
post-extract:
	@${RM} -r ${WRKSRC}/vendor/github.com/Azure/go-autorest/autorest
	@${RLN} ${WRKSRC_azure_go_autorest_autorest}/autorest ${WRKSRC}/vendor/github.com/Azure/go-autorest/autorest
	@${RM} -r ${WRKSRC}/vendor/github.com/Azure/go-autorest/autorest/adal
	@${RLN} ${WRKSRC_azure_go_autorest_adal}/autorest/adal ${WRKSRC}/vendor/github.com/Azure/go-autorest/autorest/adal
	@${RM} -r ${WRKSRC}/vendor/github.com/Azure/go-autorest/autorest/date
	@${RLN} ${WRKSRC_azure_go_autorest_date}/autorest/date ${WRKSRC}/vendor/github.com/Azure/go-autorest/autorest/date
	@${RM} -r ${WRKSRC}/vendor/github.com/Azure/go-autorest/logger
	@${RLN} ${WRKSRC_azure_go_autorest_logger}/logger ${WRKSRC}/vendor/github.com/Azure/go-autorest/logger
	@${RM} -r ${WRKSRC}/vendor/github.com/Azure/go-autorest/tracing
	@${RLN} ${WRKSRC_azure_go_autorest_tracing}/tracing ${WRKSRC}/vendor/github.com/Azure/go-autorest/tracing

post-install:
	${MKDIR} ${STAGEDIR}${PREFIX}/www/${PORTNAME}

.include <bsd.port.mk>

