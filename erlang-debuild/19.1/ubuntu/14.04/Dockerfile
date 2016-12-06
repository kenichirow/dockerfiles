FROM ubuntu:14.04

MAINTAINER hiroshi tadokoro <hiroshi.tadokoro@gu3.co.jp>

RUN locale-gen ja_JP.UTF-8 \
  && update-locale LC_ALL=ja_JP.UTF-8
ENV LC_ALL ja_JP.UTF-8

ENV OTP_VERSION 19.1

RUN apt-get update \
  && apt-get install -y \
         build-essential \
         git \
         curl \
         libssl-dev \
         ncurses-dev \
         build-essential fakeroot devscripts debhelper \
  && apt-get clean \
  && rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

RUN curl -sSL "http://www.erlang.org/download/otp_src_${OTP_VERSION}.tar.gz" -o /usr/local/src/otp_src_${OTP_VERSION}.tar.gz \
  && cd /usr/local/src \
  && echo '9f83a442de96c075a7cd1c42ceae9e3ce44b8f76 *otp_src_19.1.tar.gz' | sha1sum -c \
  && tar xf otp_src_${OTP_VERSION}.tar.gz \
  && cd otp_src_${OTP_VERSION} \
  && ./configure --prefix=/opt/erlang-${OTP_VERSION} \
                 --enable-kernel-poll \
                 --enable-hipe \
                 --enable-dirty-schedulers \
                 --enable-smp-support \
                 --enable-m64-build \
                 --enable-sharing-preserving \
                 --without-javac \
                 --disable-native-libs \
                 --disable-vm-probes \
                 --disable-megaco-flex-scanner-lineno \
                 --disable-megaco-reentrant-flex-scanner \
                 --disable-sctp \
  && make \
  && make install \
  && cd .. \
  && rm -rf otp_src_${OTP_VERSION} \
  && rm otp_src_${OTP_VERSION}.tar.gz

ENV PATH /opt/erlang-${OTP_VERSION}/bin:$PATH

WORKDIR /
