FROM ubuntu:14.04
MAINTAINER Slawomir Rozbicki <docker@rozbicki.eu>

ENV PAKPATH /root/etlegacy/etmain
ENV PAKMIRROR http.kernwaffe.de/et/etmain

# Install deps
RUN dpkg --add-architecture i386 &&  apt-get update -y \
&& sed -i 's/deb /deb [arch=amd64,i386] /g' /etc/apt/sources.list \
&& apt-get install -y --no-install-recommends \
build-essential cmake libjpeg-dev libcurl4-openssl-dev libogg-dev \
libglew-dev libglew1.10 libglu1-mesa:i386 libjpeg-turbo8:i386 \
liblua5.1-0-dev libts-dev libts-0.0-0:i386 gcc-multilib \
g++-multilib multiarch-support libsdl1.2-dev libsdl1.2debian:i386 wget \
autoconf libtool nasm automake git

# Make symlinks (needed for compilation)
RUN ln -s /usr/lib/i386-linux-gnu/libts-0.0.so.0 /lib/i386-linux-gnu/libts.so \
&& ln -s /usr/include/x86_64-linux-gnu/lua5.1-deb-multiarch.h /usr/include/ \
&& ln -s /usr/lib/i386-linux-gnu/libX11.so.6 /usr/lib/i386-linux-gnu/libX11.so \
&& ln -s /usr/lib/i386-linux-gnu/libSM.so.6 /usr/lib/i386-linux-gnu/libSM.so \
&& ln -s /usr/lib/i386-linux-gnu/libICE.so.6 /usr/lib/i386-linux-gnu/libICE.so \
&& ln -s /usr/lib/i386-linux-gnu/libXext.so.6 /usr/lib/i386-linux-gnu/libXext.so \
&& ln -s /usr/lib/i386-linux-gnu/mesa/libGL.so.1 /lib/i386-linux-gnu/libGL.so \
&& ln -s /usr/lib/i386-linux-gnu/libGLU.so.1 /lib/i386-linux-gnu/libGLU.so \
&& ln -s /usr/lib32/i386-linux-gnu/liblua5.1.so /lib/i386-linux-gnu/ \
&& ln -s /usr/lib/i386-linux-gnu/libvorbis.so.0  /usr/lib/i386-linux-gnu/libvorbis.so \
&& ln -s /usr/lib/i386-linux-gnu/libogg.so.0  /usr/lib/i386-linux-gnu/libogg.so \
&& ln -s /usr/lib/i386-linux-gnu/libSDL-1.2.so.0 /usr/lib/i386-linux-gnu/libSDL.so 

# Compile etlegacy
WORKDIR /usr/src
RUN git clone https://github.com/etlegacy/etlegacy.git
WORKDIR /usr/src/etlegacy
RUN git submodule init && git submodule update \
&& LDFLAGS="-ldl -lm $LDFLAGS" ./easybuild.sh

# Download pak files
RUN mkdir -p $PAKPATH 
WORKDIR $PAKPATH
RUN wget http://$PAKMIRROR/pak0.pk3 \
&& wget http://$PAKMIRROR/pak1.pk3 \
&& wget http://$PAKMIRROR/pak2.pk3 \
&& wget http://$PAKMIRROR/mp_bin.pk3
WORKDIR /root/etlegacy

