FROM oraclelinux:7-slim
LABEL maintainer "Bitnami <containers@bitnami.com>"

ENV HOME="/" \
    OS_ARCH="x86_64" \
    OS_FLAVOUR="ol-7" \
    OS_NAME="linux"

COPY prebuildfs /
# Install required system packages and dependencies
RUN install_packages ca-certificates curl glibc gzip hostname libaio-devel libgcc procps-ng sudo tar which zlib
RUN . ./libcomponent.sh && component_unpack "java" "1.8.232-0" --checksum fbac74363c807fce14538c5f9a9232602adc7883c1c5936571c741625de2479e
RUN . ./libcomponent.sh && component_unpack "tomcat" "9.0.27-0" --checksum 488a8fcddcd600ae8c9f32bb55ed4cf6f25d35d1e960b1aecc2b6391b6a30319
RUN curl --silent -L https://github.com/tianon/gosu/releases/download/1.11/gosu-amd64 > /usr/local/bin/gosu && echo 0b843df6d86e270c5b0f5cbd3c326a04e18f4b7f9b8457fa497b0454c4b138d7 /usr/local/bin/gosu | sha256sum --check && chmod u+x /usr/local/bin/gosu && mkdir -p /opt/bitnami/licenses && curl --silent -L https://raw.githubusercontent.com/tianon/gosu/master/LICENSE > /opt/bitnami/licenses/gosu-1.11.txt

COPY rootfs /
RUN /postunpack.sh
ENV BITNAMI_APP_NAME="tomcat" \
    BITNAMI_IMAGE_VERSION="9.0.27-ol-7-r27" \
    PATH="/opt/bitnami/java/bin:/opt/bitnami/tomcat/bin:$PATH"

EXPOSE 8080

USER 1001
ENTRYPOINT [ "/entrypoint.sh" ]
CMD [ "/run.sh" ]
