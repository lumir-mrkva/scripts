# query-exporter Dockerfile
FROM python:3-alpine

# metadata                                                                                                                                                           
ARG VCS_REF                                                                                                                                                          
ARG BUILD_DATE


LABEL io.parity.image.authors="devops-team@parity.io" \
  io.parity.image.vendor="Parity Technologies" \
	io.parity.image.title="parity/query-exporter" \
	io.parity.image.source="https://github.com/paritytech/polkadot/blob/${VCS_REF}/scripts/docker/Dockerfile" \
	io.parity.image.revision="${VCS_REF}" \                                                                                                                            
  io.parity.image.created="${BUILD_DATE}"

RUN \
  apk add --no-cache postgresql-libs && \
	apk add --no-cache --virtual .build-deps gcc musl-dev postgresql-dev && \
	python3 -m pip install --no-cache-dir SQLAlchemy[postgresql] query-exporter && \
	apk --purge del .build-deps


EXPOSE 9560

ENTRYPOINT ["python3", "/usr/local/bin/query-exporter"]
