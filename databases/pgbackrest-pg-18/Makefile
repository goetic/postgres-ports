PORTNAME=	pgbackrest
DISTVERSIONPREFIX=	release/
DISTVERSION=	2.58.0
CATEGORIES=	databases
PORTREVISION=	1
PKGNAMESUFFIX= -pg-18

MAINTAINER=	admin@goetic.dev
COMMENT=	Reliable PostgreSQL Backup & Restore
WWW=		https://pgbackrest.org/

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE

LIB_DEPENDS=	liblz4.so:archivers/liblz4 \
		libyaml.so:textproc/libyaml \
		libpq.so.5:databases/postgresql18-client

USES=		gnome meson pgsql:18,build pkgconfig python ssl
USE_GITHUB=	yes
USE_GNOME=	libxml2
RUN_DEPENDS+=   postgresql18-client>0:databases/postgresql18-client

MESON_ARGS+=	-Dconfigdir="${ETCDIR}"

BINARY_ALIAS=	python3=${PYTHON_CMD}

OPTIONS_DEFINE=		SFTP ZSTD

SFTP_DESC=		Enable SFTP storage support

SFTP_LIB_DEPENDS=	libssh2.so:security/libssh2
SFTP_MESON_ON=		-Dlibssh2=enabled
SFTP_MESON_OFF=		-Dlibssh2=disabled

ZSTD_LIB_DEPENDS=	libzstd.so:archivers/zstd
ZSTD_MESON_ON=		-Dlibzstd=enabled
ZSTD_MESON_OFF=		-Dlibzstd=disabled

post-install:
	${MKDIR} ${STAGEDIR}${ETCDIR}

.include <bsd.port.mk>

