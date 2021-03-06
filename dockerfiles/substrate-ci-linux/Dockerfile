FROM registry.parity.io/parity/infrastructure/scripts/base-ci-linux:latest

# metadata
ARG VCS_REF
ARG BUILD_DATE

LABEL io.parity.image.authors="devops-team@parity.io" \
	io.parity.image.vendor="Parity Technologies" \
	io.parity.image.title="registry.parity.io/parity/infrastructure/scripts/substrate-ci-linux" \
	io.parity.image.description="Inherits from base-ci-linux; chromium-driver; \
wasm-gc, wasm-bindgen cargo-deny" \
	io.parity.image.source="https://github.com/paritytech/scripts/blob/${VCS_REF}/\
dockerfiles/rust-builder/Dockerfile" \
	io.parity.image.documentation="https://github.com/paritytech/scripts/blob/${VCS_REF}/\
dockerfiles/rust-builder/README.md" \
	io.parity.image.revision="${VCS_REF}" \
	io.parity.image.created="${BUILD_DATE}"

WORKDIR /builds

# install tools and dependencies
RUN set -eux; \
	apt-get -y update; \
	apt-get install -y --no-install-recommends \
		chromium-driver; \
# install cargo tools
	cargo install cargo-audit cargo-web wasm-pack cargo-deny; \
# TODO: install published version once 0.2.60 gets released
	cargo install wasm-bindgen-cli; \
# install wasm toolchain
	rustup target add wasm32-unknown-unknown; \
	rustup target add wasm32-unknown-unknown --toolchain nightly; \
# install wasm-gc. It's useful for stripping slimming down wasm binaries (polkadot)
	cargo +nightly install wasm-gc; \
# versions
	rustup show; \
	cargo --version; \
# apt clean up
	apt-get autoremove -y; \
	apt-get clean; \
	rm -rf /var/lib/apt/lists/*; \
# cargo clean up
# removes compilation artifacts cargo install creates (>250M)
	rm -rf $CARGO_HOME/registry; \
# removes toolchain's html docs and autocompletions (>300M for each toolchain)
	rm -rf /usr/local/rustup/toolchains/*/share
