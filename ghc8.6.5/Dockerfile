FROM haskell:8.6.5

RUN stack upgrade && stack --resolver ghc-8.6.5 setup

RUN apt-get update -qq -y && apt-get -y install \
    libicu-dev libtinfo-dev libgmp-dev git

RUN git clone https://github.com/haskell/haskell-ide-engine --recurse-submodules

WORKDIR /haskell-ide-engine

# Ghc x.x.x -> Ghc 8.6.5 (lts-14.12)
RUN sed -i "s/lts-[0-9][0-9].[0-9][0-9]/lts-14.12/" install/shake.yaml

# Some reason shake is older version or something...
RUN echo "allow-newer: true" >> /root/.stack/config.yaml

RUN stack ./install.hs hie-8.6.5
RUN stack ./install.hs build-data
