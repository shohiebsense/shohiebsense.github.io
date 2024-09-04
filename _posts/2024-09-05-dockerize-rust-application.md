Simply you can just docker init and let it generate the holy trinity (compose, dockerignore and Dockerfile) doesn't it?  

You then find some dissatisfaction, the size is so big, security issues regarding user privilege or anything.  

You then got the idea to multi-stage it.  

This seems good [https://medium.com/@pabloperezaradros/creating-lightweight-docker-images-with-rust-0db47cb014a9](https://medium.com/@pabloperezaradros/creating-lightweight-docker-images-with-rust-0db47cb014a9)

Until you realize the rust application, its generated build (bin/bash) uses dynamic linking with C library.   

You have to add some parameters / additional scripts to command the cargo cli to make the generated rust app using static linking.  

`rustup target add x86_64-unknown-linux-musl`  
`cargo build --target x86_64-unknown-linux-musl --release`  

Your pain doesn't end here.  

`linking with cc failed`,  

`as the target x86_64-unknown-linux-gnu does not support these crate types`  

If you decide to use `FROM SCRATCH`, those are some difficulties you are likely to get.  


well have a look for reference at here  

```Dockerfile
FROM rust:1.80.1-alpine AS builder
RUN apk add --no-cache build-base perl

WORKDIR /app
COPY rust-toolchain.toml .
RUN rustup component add clippy rustfmt


FROM builder AS dependency_builder
WORKDIR /app

ENV CRATES="common director distributor receiver"
RUN printf "${CRATES}" | tr ' ' '\n' | xargs -I{} sh -c 'mkdir -p crates/{}/src && echo "fn main() { }" > crates/{}/src/main.rs && touch crates/{}/src/lib.rs'

# awaiting release of https://github.com/moby/buildkit/pull/3001
#COPY --parents --link ./Cargo.* ./crates/*/Cargo.toml ./
COPY --link "Cargo.lock" "Cargo.toml" ./
COPY --link "crates/common/Cargo.toml" crates/common/Cargo.toml
COPY --link "crates/director/Cargo.toml" crates/director/Cargo.toml
COPY --link "crates/distributor/Cargo.toml" crates/distributor/Cargo.toml
COPY --link "crates/receiver/Cargo.toml" crates/receiver/Cargo.toml

RUN cargo build --color "auto" --release --locked


FROM builder AS application_builder
WORKDIR /app

COPY --from=dependency_builder /app/target target
RUN find target -name '*saasaparilla*' -type f -delete
COPY . .
# TODO: add https://github.com/qdrant/qdrant/pull/1856/files as a just script to increase speed of multistage build
# TODO: add https://github.com/qdrant/qdrant/pull/1859/files to further increase speed of multistage builds
#       NOTE: this should only be for PR builds used for unit/integration testing
#             dev/stg/prod builds should be identical release objects
# TODO: add `--out-dir /app/bin` once `--out-dir` is stabilized to reduce size of multistage build
ARG COMPONENT
ENV COMPONENT_BIN="saasaparilla-notification-${COMPONENT}"
RUN cargo build --future-incompat-report --color "auto" --bin "${COMPONENT_BIN}" --release --locked


# https://hub.docker.com/_/rust
FROM alpine:3.19 AS final
WORKDIR /app

COPY --link LICENSE /app/LICENSE

ARG COMPONENT
ENV COMPONENT_BIN="saasaparilla-notification-${COMPONENT}"
COPY --from=application_builder --link "/app/target/release/${COMPONENT_BIN}" "/app/bin"
COPY --link "crates/${COMPONENT}/config.toml" "/app/config.toml"
CMD ["/app/bin", "config-file-path=config.toml"]


FROM scratch AS minimal
WORKDIR /app

# generate the list of required libs with `ldd /app/bin`
COPY --from=final --link "/lib/ld-musl-x86_64.so.1" /lib/

COPY --from=final --link "/app/" /app/
CMD ["/app/bin", "config-file-path=config.toml"]

```

[this is the source](https://github.com/SaaSaparilla/saasaparilla.notification/blob/master/docker/Dockerfile)  

study it.  

[https://github.com/tbillington/rust-docker-cheatsheet](https://github.com/tbillington/rust-docker-cheatsheet)  

you can use distroless.cc  

[https://users.rust-lang.org/t/rust-and-docker/77921/10](https://users.rust-lang.org/t/rust-and-docker/77921/10)  




If you don't really that care about the size, I recommend using Debian. 

```Dockerfile
ARG RUST_VERSION=1.80.1-bookworm
ARG APP_NAME=event_service


FROM rust:${RUST_VERSION} AS build
ARG APP_NAME
WORKDIR /application

COPY . .
RUN --mount=type=bind,source=src,target=src \
    --mount=type=bind,source=Cargo.toml,target=Cargo.toml \
    --mount=type=cache,target=/app/target/ \
    --mount=type=cache,target=/usr/local/cargo/git/db \
    --mount=type=cache,target=/usr/local/cargo/registry/ \
cargo install --path . && \
cp ./target/release/$APP_NAME /bin/server

FROM debian:stable-slim  AS final
WORKDIR /app
RUN apt update \
    #&& apt install -y build-essential libpq-dev libc6-dev \
    && apt install -y build-essential libpq-dev \
    && apt clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


ARG UID=10001
RUN adduser \
    --disabled-password \
    --gecos "" \
    --home "/nonexistent" \
    --shell "/sbin/nologin" \
    --no-create-home \
    --uid "${UID}" \
    appuser
USER appuser

COPY --from=build /bin/server /bin/

EXPOSE 8080

CMD ["/bin/server"]

```

build essentials is what alpine 

```Dockerfile
RUN apk update
&& apk add --virtual build-dependencies
build-base
gcc
wget
git
```

is. 

so you get the idea.  

[https://github.com/gliderlabs/docker-alpine/issues/24](https://github.com/gliderlabs/docker-alpine/issues/24)  

[if you have some time to read](https://www.reddit.com/r/rust/comments/1bviuyg/a_practical_guide_to_containerize_rust/)

[https://www.reddit.com/r/rust/comments/16bswvl/looking_for_the_perfect_dockerfile_for_rust/](https://www.reddit.com/r/rust/comments/16bswvl/looking_for_the_perfect_dockerfile_for_rust/)  

If you think it is too much just back to the basic man,  

[https://docs.docker.com/language/rust/build-images/](https://docs.docker.com/language/rust/build-images/)  

