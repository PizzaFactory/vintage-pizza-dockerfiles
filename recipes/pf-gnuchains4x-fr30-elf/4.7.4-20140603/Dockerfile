FROM camino.azurecr.io/vintage-pizza-partial/pf-gnuchains4x-fr30-elf:4.7.4-20140603 as toolchain

FROM camino.azurecr.io/eclipse/cpp_gcc:ubuntu-xenial

USER root
COPY --from=toolchain /opt/pizza/ /opt/pizza/
COPY --from=toolchain /opt/sources/* /opt/sources/
USER user

