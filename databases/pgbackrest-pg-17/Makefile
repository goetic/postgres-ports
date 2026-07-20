PORTNAME=	pgbackrest
CATEGORIES=	databases
DISTVERSIONPREFIX=	release/
PKGNAMESUFFIX= -pg-17
PORTREVISION=	0
PORTVERSION=	2.59.0

MASTER_SITES=	https://github.com/pgbackrest/pgbackrest/releases/download/release%2F${PORTVERSION}/
DISTNAME=	${PORTNAME}-${PORTVERSION}

MAINTAINER=	admin@goetic.dev
COMMENT=	Reliable PostgreSQL Backup & Restore
WWW=		https://pgbackrest.org/

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE

LIB_DEPENDS=	liblz4.so:archivers/liblz4 \
		libyaml.so:textproc/libyaml \
		libpq.so.5:databases/postgresql17-client

USES=		gnome meson pgsql:17,build pkgconfig python ssl
USE_GNOME=	libxml2
RUN_DEPENDS+=   postgresql17-client>0:databases/postgresql17-client

MESON_ARGS+=	-Dconfigdir="${ETCDIR}" -Dlibsystemd=disabled

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

