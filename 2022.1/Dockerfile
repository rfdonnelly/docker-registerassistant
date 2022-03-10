# Use a multi-stage build to prevent having to carry forward the tar-gzip
# package
ARG PACKAGE_NAME=registerassistant
ARG PACKAGE_VERSION=2022.1
ARG PACKAGE_ROOT=/opt/mentor/hds/$PACKAGE_VERSION/$PACKAGE_NAME

FROM centos:7 as intermediate

ARG PACKAGE_NAME
ARG PACKAGE_VERSION
ARG PACKAGE_ROOT
ENV PACKAGE_ROOT=$PACKAGE_ROOT

# Install package
COPY $PACKAGE_NAME-$PACKAGE_VERSION.tar.gz /tmp
RUN tar xf /tmp/$PACKAGE_NAME-$PACKAGE_VERSION.tar.gz --directory /

FROM centos:7

ARG PACKAGE_ROOT
COPY --from=intermediate $PACKAGE_ROOT $PACKAGE_ROOT

ARG PACKAGE_ROOT
ENV PACKAGE_ROOT=$PACKAGE_ROOT
ENV PATH=$PACKAGE_ROOT:$PATH

ENTRYPOINT ["regassist"]
