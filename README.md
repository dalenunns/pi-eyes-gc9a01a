# pi-eyes-gc9a01a

A version of [Adafruit's Pi_Eyes](https://github.com/adafruit/Pi_Eyes) project with support for `gc9a01a` based 240x240 round displays.

In particular these [CMU ROUND 1.28IN RGBLCD DISPLAY - Communica [Part No: CMU ROUND 1.28IN RGBLCD DISPLAY]](https://www.communica.co.za/products/cmu-round-1-28in-rgblcd-display)

Currently this only includes the `fbx2` changes and code as the original Python code for generating the eyes no longer works. (Pi3D issues)

This code will take the framebuffer (`/dev/fb0`), split it and send each side out to the two displays.

You can enable gc9a01a mode by running `fbx2 -g`

Below is a working `/boot/config.txt` for my Pi3B, this is based on the changes made by the original install file however I needed to comment out the following to get access to the framebuffer.

```
# Enable DRM VC4 V3D driver
#dtoverlay=vc4-kms-v3d
#max_framebuffers=2
```

Original `/boot/config.txt`
```
# For more options and information see
# http://rpf.io/configtxt
# Some settings may impact device functionality. See link above for details

# uncomment if you get no picture on HDMI for a default "safe" mode
#hdmi_safe=1

# uncomment the following to adjust overscan. Use positive numbers if console
# goes off screen, and negative if there is too much border
#overscan_left=16
#overscan_right=16
#overscan_top=16
#overscan_bottom=16

# uncomment to force a console size. By default it will be display's size minus
# overscan.
#framebuffer_width=1280
#framebuffer_height=720

# uncomment if hdmi display is not detected and composite is being output
hdmi_force_hotplug=1

# uncomment to force a specific HDMI mode (this will force VGA)
hdmi_group=2
hdmi_mode=87

# uncomment to force a HDMI mode rather than DVI. This can make audio work in
# DMT (computer monitor) modes
#hdmi_drive=2

# uncomment to increase signal to HDMI, if you have interference, blanking, or
# no display
#config_hdmi_boost=4

# uncomment for composite PAL
#sdtv_mode=2

#uncomment to overclock the arm. 700 MHz is the default.
#arm_freq=800

# Uncomment some or all of these to enable the optional hardware interfaces
#dtparam=i2c_arm=on
#dtparam=i2s=on
dtparam=spi=on

# Uncomment this to enable infrared communication.
#dtoverlay=gpio-ir,gpio_pin=17
#dtoverlay=gpio-ir-tx,gpio_pin=18

# Additional overlays and parameters are documented /boot/overlays/README

# Enable audio (loads snd_bcm2835)
dtparam=audio=on

# Automatically load overlays for detected cameras
camera_auto_detect=1

# Automatically load overlays for detected DSI displays
display_auto_detect=1

# Enable DRM VC4 V3D driver
#dtoverlay=vc4-kms-v3d
#max_framebuffers=2

# Disable compensation for displays with overscan
disable_overscan=1

[cm4]
# Enable host mode on the 2711 built-in XHCI USB controller.
# This line should be removed if the legacy DWC2 controller is required
# (e.g. for USB device mode) or if USB support is not required.
otg_mode=1

[all]

[pi4]
# Run as fast as firmware / board allows
arm_boost=1

[all]
gpu_mem=128
hdmi_cvt=1280 720 60 1 0 0 0
dtparam=spi1=on
dtoverlay=spi1-3cs
```