FROM alpine:3.20 AS package

ARG APP=airupnp
ARG TARGETARCH
ARG VERSION=1.10.1

WORKDIR /src

RUN apk add --no-cache unzip

COPY AirConnect-${VERSION}.zip .

RUN set -eux; \
	case "$APP" in \
		aircast|airupnp) ;; \
		*) echo "Unsupported APP: $APP" >&2; exit 1 ;; \
	esac; \
	case "$TARGETARCH" in \
		amd64) airconnect_arch="x86_64" ;; \
		arm64) airconnect_arch="aarch64" ;; \
		*) echo "Unsupported TARGETARCH: $TARGETARCH" >&2; exit 1 ;; \
	esac; \
	unzip "AirConnect-${VERSION}.zip" "${APP}-linux-${airconnect_arch}-static"; \
	mv "${APP}-linux-${airconnect_arch}-static" /airconnect; \
	chmod 0755 /airconnect

FROM scratch

ARG APP=airupnp
ARG VERSION=1.10.1

LABEL org.opencontainers.image.title="AirConnect ${APP}" \
      org.opencontainers.image.description="AirConnect ${APP} bridge packaged from the upstream static Linux release binary." \
      org.opencontainers.image.source="https://github.com/yuejunfeng0909/AirConnect" \
      org.opencontainers.image.version="${VERSION}" \
      org.opencontainers.image.licenses="MIT"

COPY --from=package /airconnect /airconnect

ENTRYPOINT ["/airconnect"]
CMD ["-Z"]
