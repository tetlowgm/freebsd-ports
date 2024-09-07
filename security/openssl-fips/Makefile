PORTNAME=	openssl
PORTVERSION=	3.0.9
CATEGORIES=	security devel
MASTER_SITES=	https://www.openssl.org/source/ \
		ftp://ftp.cert.dfn.de/pub/tools/net/openssl/source/
PKGNAMESUFFIX=	-fips

MAINTAINER=	gordon@FreeBSD.org
COMMENT=	FIPS module for OpenSSL
WWW=		https://openssl-library.org/

LICENSE=	APACHE20
LICENSE_FILE=	${WRKSRC}/LICENSE.txt

EXPIRATION_DATE=	2026-09-21
BROKEN_SSL=	libressl libressl-devel openssl111
BROKEN_SSL_REASON=	requires OpenSSL version 3.0 or higher
USES=		perl5
USE_PERL5=	build

PORTSCOUT=	ignore:1

HAS_CONFIGURE=	yes
CONFIGURE_SCRIPT=	Configure
CONFIGURE_ENV=	PERL="${PERL}"
CONFIGURE_ARGS=	enable-fips

.include <bsd.port.pre.mk>

.if ${SSL_DEFAULT} == base && ${OSVERSION} < 1400092
IGNORE=	base OpenSSL needs to be OpenSSL 3.0 or higher
.endif

do-install:
	${MKDIR} ${STAGEDIR}${PREFIX}/lib/ossl-modules
	${INSTALL_LIB} ${WRKSRC}/providers/fips.so ${STAGEDIR}${PREFIX}/lib/ossl-modules/fips.so

#post-install:
#	openssl fipsinstall -module ${STAGEDIR}${PREFIX}/lib/ossl-modules/fips.so -provider_name fips -section_name fips_sect -out ${STAGEDIR}${PREFIX}/etc/fipsmodule.cnf
.include <bsd.port.post.mk>
