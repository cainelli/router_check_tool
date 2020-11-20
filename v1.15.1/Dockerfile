FROM ubuntu as builder

ENV ENVOY_TAG v1.15.1

# Build dependencies
RUN apt-get update -y && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    curl \
    gnupg \
    python3 \
    python3-pip \
    dh-autoreconf \
    git \
    libtool \
    automake \
    autoconf \
    make \
    ninja-build \
    unzip \
    virtualenv \
    cmake

RUN git clone https://github.com/envoyproxy/envoy.git

WORKDIR /envoy


# Install bazel
RUN curl -fsSL https://bazel.build/bazel-release.pub.gpg | gpg --dearmor > bazel.gpg
RUN mv bazel.gpg /etc/apt/trusted.gpg.d/
RUN echo "deb [arch=amd64] https://storage.googleapis.com/bazel-apt stable jdk1.8" | tee /etc/apt/sources.list.d/bazel.list
RUN apt-get update -y && apt-get install bazel-3.1.0 -y

# Build
RUN git checkout ${ENVOY_TAG}
<<<<<<< HEAD
=======
# additional extensions
COPY v1.15.1/BUILD /envoy/test/tools/router_check/BUILD
>>>>>>> 7abe52d06f86320002411fe31a907e57e9f0f4d6
RUN bazel-3.1.0 build //test/tools/router_check:router_check_tool

FROM ubuntu

COPY --from=builder /envoy/bazel-bin/test/tools/router_check/router_check_tool /usr/local/bin/

RUN apt-get update && apt-get install -y \
  libatomic1 \
  && rm -rf /var/lib/apt/lists/*

ENTRYPOINT [ "/usr/local/bin/router_check_tool"]
