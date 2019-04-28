FROM camino.azurecr.io/eclipse/cpp_gcc:ubuntu-xenial

USER root
RUN apt-get update && \
    apt-get install -y gcc-4.7 g++-4.7 && \
    apt-get -y clean && \
    rm -rf /var/lib/apt/lists/*
USER user
