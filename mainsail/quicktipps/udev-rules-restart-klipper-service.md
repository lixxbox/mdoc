---
description: >-
  To establish the connection, let the Klipper service restart automatically as
  soon as the printer is connected.
---

# todo: udev-rules: restart Klipper service

You have to create so called udev rules. Therefore you have to find out the ID of your board first.

### Find out board ID

```text
udevadm monitor --kernel --property --subsystem-match=usb
```

Now connect or disconnect the USB device to trigger a UDEV event.   
Note the ID that occurs after "PRODUCT=".

### Create udev rules

```text
/etc/udev/rules.d
sudo nano 98-klipper.rules
```

Paste the following content and save. Remember to replace `1d50/614e/100` in both lines with your own board ID.

```text
ACTION=="add", SUBSYSTEM=="usb", ENV{PRODUCT}=="1d50/614e/100", RUN=="/bin/systemctl --no-block restart klipper.service"
ACTION=="remove", SUBSYSTEM=="usb", ENV{PRODUCT}=="1d50/614e/100", RUN+="/bin/systemctl --no-block stop klipper.service"
```

