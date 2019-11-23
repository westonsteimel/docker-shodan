ARG SHODAN_VERSION="1.19.0"

FROM python:3-alpine

ARG SHODAN_VERSION
ENV SHODAN_VERSION "${SHODAN_VERSION}"

RUN apk --no-cache add \
	ca-certificates \
	&& pip install shodan=="${SHODAN_VERSION}" \
    && addgroup shodan \
    && adduser -G shodan -s /bin/sh -D shodan

USER shodan
WORKDIR /home/shodan/Downloads

ENTRYPOINT [ "shodan" ]

LABEL org.opencontainers.image.title="shodan" \
    org.opencontainers.image.description="shodan in Docker" \ 
    org.opencontainers.image.url="https://github.com/westonsteimel/docker-shodan" \ 
    org.opencontainers.image.source="https://github.com/westonsteimel/docker-shodan" \
    org.opencontainers.image.version="${SHODAN_VERSION}" \
    version="${SHODAN_VERSION}"

