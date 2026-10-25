FROM chmolinari/base-centos-stream:1.0.0
LABEL author="Christian Molinari" \
    version=1.0.0 \
    description="A CentOS Stream 10 Linux image for C and C++ development, based on chmolinari/base-centos-stream:1.0.0."

RUN sudo dnf update -y && \
    sudo dnf group install -y "Development Tools" && \
    sudo dnf install -y python3-pip cmake ninja-build git curl zip unzip tar pkgconf-pkg-config boost-devel && \
    sudo dnf clean all

# Conan 2.33.0, isolated from the system Python.
RUN sudo python3 -m venv /opt/conan && \
    sudo /opt/conan/bin/pip install --no-cache-dir --only-binary=:all: conan==2.33.0 && \
    sudo ln -s /opt/conan/bin/conan /usr/local/bin/conan

# vcpkg release 2026.10.16, from the upstream repository.
RUN sudo git clone https://github.com/microsoft/vcpkg.git /opt/vcpkg && \
    sudo git -C /opt/vcpkg -c advice.detachedHead=false checkout 9eec002df1cd109f8f104cd966a763daf9751489 && \
    sudo /opt/vcpkg/bootstrap-vcpkg.sh -disableMetrics && \
    sudo chown -R devuser:wheel /opt/vcpkg

ENV VCPKG_ROOT=/opt/vcpkg
ENV PATH="${VCPKG_ROOT}:${PATH}"
