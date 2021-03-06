FROM ubuntu:xenial as builder

# metadata
ARG VCS_REF
ARG BUILD_DATE

LABEL io.parity.image.authors="devops-team@parity.io" \
	io.parity.image.vendor="Parity Technologies" \
	io.parity.image.title="registry.parity.io/parity/infrastructure/scripts/parity-ci-docs" \
	io.parity.image.description="curl ca-certificates git; nodejs yarn" \
	io.parity.image.source="https://github.com/paritytech/scripts/blob/${VCS_REF}/\
dockerfiles/parity-ci-docs/Dockerfile" \
	io.parity.image.documentation="https://github.com/paritytech/scripts/blob/${VCS_REF}/\
dockerfiles/parity-ci-docs/README.md" \
	io.parity.image.revision="${VCS_REF}" \
	io.parity.image.created="${BUILD_DATE}"

WORKDIR /builds/parity/parity-ethereum/

# copy yarn repo key
COPY utility/yarn.key /etc/apt/trusted.gpg.d/debian-yarn.gpg

# install tools and dependencies
RUN set -eux; \
	apt-get -y update; \
    apt-get install -y --no-install-recommends \
		curl ca-certificates git; \
# install nodejs and yarn
	curl -sL https://deb.nodesource.com/setup_10.x | bash -; \
	echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list; \
	apt-get -y update; \
	apt-get install -y --no-install-recommends \
		nodejs yarn; \
	# apt clean up
	apt-get autoremove -y; \
	apt-get clean; \
	rm -rf /var/lib/apt/lists/*
