FROM chmolinari/base-fedora:1.0.0
LABEL author="Christian Molinari" \
    version=1.0.0 \
    description="A Fedora Linux image for C and C++ development, based on chmolinari/base-fedora:1.0.0."

RUN sudo dnf update -y && \
    sudo dnf group install -y c-development && \
    sudo dnf install -y cmake ninja-build conan && \
    sudo dnf clean all