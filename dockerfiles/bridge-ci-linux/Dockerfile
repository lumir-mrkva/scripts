FROM registry.parity.io/parity/infrastructure/scripts/parity-ci-linux:latest

# metadata
ARG VCS_REF
ARG BUILD_DATE

LABEL io.parity.image.authors="devops-team@parity.io" \
	io.parity.image.vendor="Parity Technologies" \
	io.parity.image.title="registry.parity.io/parity/infrastructure/scripts/bridge-ci-linux" \
	io.parity.image.description="Inherits from parity-ci-linux. \
rust stable, rust nightly, cargo-audit, sccache (redis)" \
	io.parity.image.source="https://github.com/paritytech/scripts/blob/${VCS_REF}/\
dockerfiles/bridge-ci-linux/Dockerfile" \
	io.parity.image.documentation="https://github.com/paritytech/scripts/blob/${VCS_REF}/\
dockerfiles/bridge-ci-linux/README.md" \
	io.parity.image.revision="${VCS_REF}" \
	io.parity.image.created="${BUILD_DATE}"

WORKDIR /builds

#install Parity Ethereum
ADD "https://releases.parity.io/ethereum/stable/x86_64-unknown-linux-gnu/parity" /usr/bin/
RUN chmod +x /usr/bin/parity; \
#instal Solidity Compiler
	set -eux; \
	snap install solc

# compiler ENV
ENV CC=clang \
	CXX=clang \
# cache handler
	RUSTC_WRAPPER=sccache \
# show backtraces
	RUST_BACKTRACE=1
