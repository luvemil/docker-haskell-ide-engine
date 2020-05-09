FROM haskell:8.8.2

RUN stack upgrade && stack --resolver ghc-8.8.2 setup

RUN apt-get update -qq -y && apt-get -y install \
    libicu-dev libtinfo-dev libgmp-dev git

RUN git clone https://github.com/haskell/haskell-ide-engine --recurse-submodules

WORKDIR /haskell-ide-engine

# Ghc x.x.x -> Ghc 8.8.2 (lts-15.3)
RUN sed -i "s/lts-[0-9][0-9].[0-9][0-9]/lts-15.3/" install/shake.yaml

# Some reason shake is older version or something...
RUN echo "allow-newer: true" >> /root/.stack/config.yaml

RUN stack ./install.hs hie-8.8.2
RUN stack install hoogle && stack ./install.hs data