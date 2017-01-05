FROM ubuntu:16.04

MAINTAINER Shigemasa Watanabe <shigemasa.watanabe@gu3.co.jp>

RUN locale-gen ja_JP.UTF-8 \
  && update-locale LC_ALL=ja_JP.UTF-8
ENV LC_ALL ja_JP.UTF-8

ENV OTP_VERSION 19.2
ENV ELIXIR_VERSION 1.4.0

RUN apt-get update \
  && apt-get install -y \
         build-essential \
         git \
         curl \
         libssl-dev \
         ncurses-dev \
  && apt-get clean \
  && rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

RUN curl -sSL "http://www.erlang.org/download/otp_src_${OTP_VERSION}.tar.gz" -o /usr/local/src/otp_src_${OTP_VERSION}.tar.gz \
  && cd /usr/local/src \
  && echo 'f5188ba6f496b9d1c37597705d095b4e6aa7bcd3 *otp_src_19.2.tar.gz' | sha1sum -c \
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


ENV PREFIX /opt/elixir-$ELIXIR_VERSION

RUN curl -sSL https://github.com/elixir-lang/elixir/archive/v$ELIXIR_VERSION.tar.gz -o /usr/local/src/elixir-$ELIXIR_VERSION.tar.gz \
  && cd /usr/local/src \
  && echo '4b8503598f65c19cb40bcae3e1e40726487e2230 *elixir-1.4.0.tar.gz' | sha1sum -c \
  && tar xf elixir-$ELIXIR_VERSION.tar.gz \
  && cd elixir-$ELIXIR_VERSION \
  && make \
  && make install \
  && cd .. \
  && rm -rf elixir-$ELIXIR_VERSION \
  && rm -rf elixir-$ELIXIR_VERSION.tar.gz


ENV PATH /opt/elixir-${ELIXIR_VERSION}/bin:$PATH

WORKDIR /
