ARG PYTHON_VERSION=3.13

FROM python:${PYTHON_VERSION}-slim-bookworm AS python-builder

RUN mkdir -p /deps && \
    ldd $(which python) | awk '{print $3}' | grep -v '^(' | xargs -I '{}' cp -v '{}' /deps/ || true

FROM gcr.io/distroless/cc-debian12:nonroot

ARG PYTHON_VERSION=3.13

LABEL org.opencontainers.image.title="Distroless Python Base" \
      org.opencontainers.image.version="${PYTHON_VERSION}" \
      org.opencontainers.image.description="Minimal Python base image built from distroless with CPython ${PYTHON_VERSION}" \
      org.opencontainers.image.vendor="Whoever"
    
COPY --from=python-builder /usr/local/lib/ /usr/local/lib/
COPY --from=python-builder /usr/local/bin/python /usr/local/bin/python
COPY --from=python-builder /etc/ld.so.cache /etc/ld.so.cache

COPY --from=python-builder /deps/ /

ENV LANG=C.UTF-8 \
    LC_ALL=C.UTF-8 \
    PYTHONDONTWRITEBYTECODE=1 \
    PYTHONFAULTHANDLER=1 \
    PYTHONUNBUFFERED=1

USER nonroot:nonroot

ENTRYPOINT ["/usr/local/bin/python"]