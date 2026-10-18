FROM fedora:44
LABEL author="Christian Molinari" \
    version=1.0.0 \
    description="A base Fedora Linux image based on fedora:44."

RUN dnf update -y && \
    dnf install -y sudo && \
    dnf clean all

# === DEVELOPMENT LAYER ===

# Container user for development.
RUN useradd -d /home/devroot -m -g wheel devuser && \
    chown devuser:wheel /home/devroot && \
    chmod 755 /home/devroot && \
    echo '%wheel ALL=(ALL) NOPASSWD: ALL' > /etc/sudoers.d/wheel-nopasswd && \
    chmod 440 /etc/sudoers.d/wheel-nopasswd && \
    visudo -cf /etc/sudoers.d/wheel-nopasswd

# Block root login: lock the password and disable the shell.
RUN usermod -L -s /sbin/nologin root

USER devuser:wheel
WORKDIR /home/devroot
