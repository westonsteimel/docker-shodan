ARG SHODAN_VERSION="master"

FROM python:3-alpine as builder

ARG SHODAN_VERSION
ENV SHODAN_VERSION "${SHODAN_VERSION}"

RUN apk add --no-cache git \
    && addgroup shodan \
    && adduser -G shodan -s /bin/sh -D shodan

USER shodan
RUN pip install --user --no-cache-dir "git+https://github.com/achillean/shodan-python@${SHODAN_VERSION}" 

FROM python:3-alpine

ARG SHODAN_VERSION

RUN addgroup shodan \
    && adduser -G shodan -s /bin/sh -D shodan

USER shodan
ENV PATH "/home/shodan/.local/bin:$PATH"
WORKDIR /home/shodan
COPY --from=builder /home/shodan/.local/ /home/shodan/.local/

ENTRYPOINT ["shodan"]
CMD ["--help"]

LABEL org.opencontainers.image.title="shodan" \
    org.opencontainers.image.description="shodan in Docker" \
    org.opencontainers.image.url="https://github.com/westonsteimel/docker-shodan" \
    org.opencontainers.image.source="https://github.com/westonsteimel/docker-shodan" \
    org.opencontainers.image.version="${SHODAN_VERSION}" \
    version="${SHODAN_VERSION}"

