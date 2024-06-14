# Fedora 40 Post Install Guide

### Faster Updates

- `sudo nano /etc/dnf/dnf.conf`
- Copy and replace the text with the following:
```bash
[main] 
gpgcheck=1 
installonly_limit=3 
clean_requirements_on_remove=True 
best=False 
skip_if_unavailable=True 
fastestmirror=1 
max_parallel_downloads=10 
deltarpm=true
```

### RPM Fusion

- Fedora has disabled the repositories for a lot of free and non-free .rpm packages by default. Follow this if you want to use non-free software like Steam, Discord and some multimedia codecs etc. As a general rule of thumb its advised to do this get access to many mainstream useful programs.
- If you forgot to enable third party repositories during the initial setup window, enable them by pasting the following into the terminal:
- `sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm`
- also while you're at it, install app-stream metadata by
- `sudo dnf groupupdate core`

### Update
- Go into the software center and click on update. Alternatively, you can use the following commands:
- `sudo dnf -u update`
- `sudo dnf -y upgrade --refresh`
- Reboot

### Battery Life
- Follow this if you have a Laptop and are facing sub optimal battery backup.
- power-profiles-daemon which come pre-configured works great on a great majority of systems but still in case you're facing sub-optimal battery backup you try installing tlp by:
- `sudo dnf install tlp tlp-rdw`
- and mask power-profiles-daemon by:
- `sudo systemctl mask power-profiles-daemon`
- Also install powertop by:
- `sudo dnf install powertop`
- `sudo powertop --auto-tune`

### Media Codecs
- Install these to get proper multimedia playback.
```bash
sudo dnf groupupdate 'core' 'multimedia' 'sound-and-video' --setopt='install_weak_deps=False' --exclude='PackageKit-gstreamer-plugin' --allowerasing && sync
sudo dnf swap 'ffmpeg-free' 'ffmpeg' --allowerasing
sudo dnf install gstreamer1-plugins-{bad-\*,good-\*,base} gstreamer1-plugin-openh264 gstreamer1-libav --exclude=gstreamer1-plugins-bad-free-devel ffmpeg gstreamer-ffmpeg
sudo dnf install lame\* --exclude=lame-devel
sudo dnf group upgrade --with-optional Multimedia
sudo dnf install vlc
```

### H/W Video Decoding with VA-API
- `sudo dnf install ffmpeg ffmpeg-libs libva libva-utils`
    - No need to do this for intel integrated graphics. Mesa drivers are for AMD graphics, who lost support for h264/h245 in the fedora repositories in f38 due to legal concerns.
        - If you have an AMD chipset, after installing the packages above do:
        - `sudo dnf swap mesa-va-drivers mesa-va-drivers-freeworld`

### Apps
- Packages for Rar and 7z compressed files support: 
    - `sudo dnf install -y unzip p7zip p7zip-plugins unrar`


