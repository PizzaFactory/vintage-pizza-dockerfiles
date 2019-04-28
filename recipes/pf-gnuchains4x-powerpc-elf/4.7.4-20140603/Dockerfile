FROM camino.azurecr.io/vintage-pizza-partial/stack-base:ubuntu-xenial
ARG RELEASE=4.7.4-20140603
ARG TARGET=powerpc-pizzafactory-elf
ARG PREFIX=/opt/pizza

USER root
RUN mkdir tmp && \
    cd tmp && \
    wget http://ftp.gnu.org/gnu/texinfo/texinfo-4.13.tar.gz && \
    tar xf texinfo-4.13.tar.gz && \
    cd texinfo-4.13 && \
    ./configure --prefix=/usr && \
    make && \
    make install && \
    cd .. && \
    rm -fr tmp
RUN apt-get update
RUN apt-get install -y bison flex gcc-4.9
RUN mkdir -p /opt/sources /tmp/sources /tmp/build ${PREFIX}
WORKDIR /opt/sources
RUN wget https://bitbucket.org/pizzafactory/pf-binutils-gdb/downloads/pf-binutils-gdb-${RELEASE}.tar.gz
WORKDIR /tmp/sources
RUN tar xf /opt/sources/pf-binutils-gdb-${RELEASE}.tar.gz
WORKDIR pf-binutils-gdb-${RELEASE}
RUN sh 00pizza-generate-link.sh
WORKDIR /tmp/build
RUN CC=gcc-4.9 CXX=g++-4.9 /tmp/sources/pf-binutils-gdb-${RELEASE}/configure --quiet --disable-werror --disable-debug --disable-dependency-tracking --disable-silent-rules --prefix=${PREFIX} --target=${TARGET} --disable-gdbtk  --disable-tui --disable-rda --enable-interwork --enable-multilib --with-newlib --without-headers --without-ppl --without-cloog --enable-languages=c,c++ --with-bugurl=http://sourceforge.jp/projects/pf3gnuchains/ticket/
RUN make all-binutils
RUN make all-ld
RUN make all-gas
RUN make all-gdb
RUN make all-sim
RUN make all-gcc
RUN make all-target-libgcc
RUN make install-binutils
RUN make install-ld
RUN make install-gas
RUN make install-gdb
RUN make install-sim
RUN make install-gcc
RUN make install-target-libgcc

USER user

# Just checking.
RUN ${PREFIX}/bin/${TARGET}-gcc --help
