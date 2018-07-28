Show system startup/shutdown logs
---------------------------------
```
gedit /etc/default/grub
update-grub
```
use `GRUB_CMDLINE_LINUX_DEFAULT=""` instead of `GRUB_CMDLINE_LINUX_DEFAULT="quiet"`
use `GRUB_GFXMODE=1920x1080` instead of use `GRUB_GFXMODE=640x480`

Disable wayland for nvidia and enable debug logs for gdm3
---------------------------------------------------------
```
dpkg -S /etc/gdm3/daemon.conf
gedit /etc/gdm3/daemon.conf
```
uncomment `WaylandEnable=false`
uncomment `Enable=true`

Update samsung monitor info to xorg
-----------------------------------
```
gtf 1920 1080 120
gedit /etc/X11/xorg.conf
```
add this line under `Monitor` --> `Modeline "1920x1080_120.00"  368.76  1920 2072 2288 2656  1080 1081 1084 1157  -HSync`
