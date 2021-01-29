---
description: >-
  Klipper is shipped with an Octoprint entry in the LCD menu. Let's be honest:
  who needs this?
---

# Disable Octoprint LCD menu

Just add the following entry to your printer.cfg:

```text
[menu __main __octoprint]
type: disabled
```

