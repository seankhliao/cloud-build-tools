FROM archlinux/base:latest AS build

WORKDIR /build
RUN mkdir -m 0755 -p dev run etc/pacman.d var/{cache/pacman/pkg,lib/pacman,log} && \
    mkdir -m 1777 -p tmp && \
    mkdir -m 0555 -p sys proc && \
    ln -s /dev/null /build/dev/null && \
    cp /etc/pacman.d/mirrorlist etc/pacman.d/mirrorlist
RUN pacman -r /build -Sy --noconfirm pacman

FROM scratch
COPY --from=build /build /
RUN pacman-key --init && \
    pacman-key --populate archlinux

ENTRYPOINT ["/bin/bash"]
