FROM firemiles/crosstool-ng
MAINTAINER Slawomir Rozbicki <docker@rozbicki.eu>

# Install some usefull apps
RUN apt-get update -y && apt-get install -y vim

# Copy config for selected arch
COPY .config /home/firemiles/

# Build crosstool-ng
RUN ct-ng build

