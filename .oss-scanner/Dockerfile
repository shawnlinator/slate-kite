FROM debian:trixie

RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential pkg-config \
    && rm -rf /var/lib/apt/lists/*

COPY . /src
WORKDIR /src

RUN make -j"$(nproc)"
