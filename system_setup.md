#. Install nvidia drivers
----------------------
1. Remove all nvidia related packages.
       sudo apt-get remove nvidia* && sudo apt autoremove
2. Now install some required dependencies:
       sudo apt-get install dkms build-essential linux-headers-generic
3. Block and disable nouveau kernel driver:
       sudo vim /etc/modprobe.d/blacklist.conf
   and append the follow lines to the blacklist.conf:
       blacklist nouveau
       blacklist lbm-nouveau
       options nouveau modeset=0
       alias nouveau off
       alias lbm-nouveau off
4. Disable the Kernel `nouveau` by typing the following commands:
       echo options nouveau modeset=0 | sudo tee -a /etc/modprobe.d/nouveau-kms.conf
   Finally update and reboot:
       sudo update-initramfs -u
       reboot
5. Add `contrib` and `non-free` components to `/etc/apt/sources.list`, for example:
       # Debian 9 "Stretch"
       deb http://httpredir.debian.org/debian/ stretch main contrib non-free
6. Update the list of available packages. Install the appropriate linux-headers and kernel module packages:
       apt update
       apt install linux-headers-$(uname -r|sed 's/[^-]*-[^-]*-//') nvidia-driver

   This will install the nvidia-driver package. `DKMS` will build the nvidia module for your system, via the nvidia-kernel-dkms package.
7. Restart your system to enable the nouveau blacklist.
8. Install `nvidis-xconfig`
       apt install nvidia-xconfig

#. Install intel wifi drivers
----------------------
1. Update the list of available packages and install the firmware-iwlwifi package:
       apt-get update && apt-get install firmware-iwlwifi

2. As the iwlwifi module is automatically loaded for supported devices, reinsert this module to access installed firmware:
       modprobe -r iwlwifi ; modprobe iwlwifi

#. Install bluetooth drivers
----------------------
1. Install Bluetooth support
       apt install bluetooth
2. To connect to a given device you need working bluetooth on your machine and the following packages, one of which is non-free software which will require you to enable the non-free repository in your `/etc/apt/source.list` file.
       apt-get install pulseaudio pulseaudio-module-bluetooth pavucontrol bluez-firmware
3. Now it may be necessary to restart the bluetooth and pulseaudio services:
       service bluetooth restart
       killall pulseaudio
4. In order to prevent GDM from capturing the A2DP sink on session start, edit `/var/lib/gdm3/.config/pulse/client.conf` (or create it, if it doesn't exist):
       autospawn = no
       daemon-binary = /bin/true
5. After that you have to grant access to this file to `Debian-gdm` user:
       chown Debian-gdm:Debian-gdm /var/lib/gdm3/.config/pulse/client.conf
6. You will also need to disable pulseaudio startup:
       rm /var/lib/gdm3/.config/systemd/user/sockets.target.wants/pulseaudio.socket
7. In order to auto-connect a2dp for some devices, add this to `/etc/pulse/default.pa`:
       load-module module-switch-on-connect
8. Reboot

#. Install atom
----------------------
1. Download latest release from https://atom.io/
2. Install the downloaded file
       dpkg -i atom-amd64.deb
       apt install -f

#. Install google chrome
----------------------
 1. Download latest release
 2. Install the downloaded file
        dpkg -i google-chrome-stable_current_amd64.deb
        apt install -f

#. Install Utilities
----------------------
1. Install sudo: `apt install sudo`
2. Install vim: `apt install vim`
3. Install git: `apt install git`
4. Install Indian fonts: `apt install fonts-indic`
5. Install dirmngr: `apt install dirmngr`
6. Install vlc: `apt install vlc`
7. Install extra multimedia codecs: `apt install libavcodec-extra`
8. Install gparted: `apt install gparted`

#. Install spotify
----------------------
1. Add the Spotify repository signing keys to be able to verify downloaded packages
       sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0DF731E45CE24F27EEEB1450EFDC8610341D9410 931FF8E79F0876134EDDBDCCA87FF9DF48BF1C90

2. Add the Spotify repository
       echo deb http://repository.spotify.com stable non-free | sudo tee /etc/apt/sources.list.d/spotify.list

3. Update list of available packages
       sudo apt-get update

4. Install Spotify
       sudo apt-get install spotify-client

#. Install VPN `windscribe`
----------------------
1. Install `dirmngr` and `apt-transport-https` if not already installed
       apt-get install dirmngr apt-transport-https
2. Add the Windscribe signing key to apt as root
       apt-key adv --keyserver keyserver.ubuntu.com --recv-key FDC247B7
4. Add the repository to your `sources.list`
       sh -c "echo 'deb https://repo.windscribe.com/debian stretch main' > /etc/apt/sources.list.d/windscribe-repo.list"
5. Run `apt-get update`
       apt-get update
6. Install `windscribe-cli`
       apt-get install windscribe-cli
7. Switch to non-root user
       exit
8. Login to Windscribe
       windscribe login
9. Connect to Windscribe
       windscribe connect
Need help?
       windscribe --help
