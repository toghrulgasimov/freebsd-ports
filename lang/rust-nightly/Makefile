# Created by: Jean-Sébastien Pédron <dumbbell@FreeBSD.org>

# Run update.sh to update to the latest nightly
PORTVERSION=	1.59.0.${NIGHTLY_DATE:C,-,,g}
# Always set PORTREVISION explicitly as otherwise it is inherited from lang/rust
PORTREVISION=	0
PKGNAMESUFFIX=	-nightly
DISTNAME=	rustc-nightly-src

ONLY_FOR_ARCHS=	amd64
ONLY_FOR_ARCHS_REASON=	upstream does not provide bootstraps for other architectures

CONFLICTS_INSTALL=	rust

MASTERDIR=	${.CURDIR}/../rust
PATCHDIR=	${.CURDIR}/files
DISTINFO_FILE=	${.CURDIR}/distinfo

NIGHTLY_DATE=		2021-12-21
BOOTSTRAPS_DATE=	2021-11-30
RUST_BOOTSTRAP_VERSION=	beta

.include "${MASTERDIR}/Makefile"
