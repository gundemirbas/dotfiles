FROM archlinux:base-devel
RUN sed -i '/ParallelDownloads/s/^#//g' /etc/pacman.conf && \
    echo -e "[multilib]\nInclude = /etc/pacman.d/mirrorlist\n" >> /etc/pacman.conf && \
    echo -e "keyserver-options auto-key-retrieve" >> /etc/pacman.d/gnupg/gpg.conf && \
    pacman --noconfirm -Syyuu && \
    pacman --noconfirm -S \
    sudo \
    nano \
    cargo \
    bluez \
    bluez-utils \
    pipewire \
    pipewire-jack \
    pipewire-alsa \
    pipewire-audio \
    pipewire-pulse \
    wireplumber \
    vulkan-radeon \
    vulkan-intel \
    lib32-vulkan-radeon \
    lib32-vulkan-intel \
    steam \
    && \
    echo "%wheel ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
    useradd gamer -G wheel -m && \
    pacman --noconfirm -S --needed git && \
    su - gamer -c "git clone https://aur.archlinux.org/paru.git /tmp/paru" && \
    su - gamer -c "cd /tmp/paru && makepkg -si --noconfirm" && \
    su - gamer -c "paru --noconfirm -S gamescope-plus lib32-gamescope-plus gamescope-session-git" && \
    su - gamer -c "paru --noconfirm -c" && \
    rm /home/gamer/* /tmp/* /var/cache* -rf
