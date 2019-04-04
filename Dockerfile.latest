FROM opensuse/tumbleweed

# do not install the files marked as documentation (use "rpm --excludedocs")
RUN sed -i -e "s/^.*rpm.install.excludedocs.*/rpm.install.excludedocs = yes/" /etc/zypp/zypp.conf

# "zypper dup" synchronizes with the current Tumbleweed (even downgrades if needed),
# see https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/#run
# https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/#/build-cache
# why we need "zypper clean -a" at the end
RUN zypper --non-interactive dup --no-recommends && zypper --non-interactive in --no-recommends \
  autoconf \
  automake \
  boost-devel \
  brp-check-suse \
  brp-extract-appdata \
  build \
  ccache \
  doxygen \
  gcc-c++ \
  git \
  graphviz \
  libboost_headers-devel \
  libboost_test-devel \
  libjson-c-devel \
  libtool \
  libxml2-devel \
  obs-service-source_validator \
  python3-devel \
  rpm-build \
  ruby-devel \
  swig \
  && zypper clean -a \
  && rm -rf /usr/share/doc/

ENV LC_ALL=en_US.UTF-8
WORKDIR /usr/src/app
