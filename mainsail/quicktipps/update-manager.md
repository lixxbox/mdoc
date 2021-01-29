---
description: 'Perform updates of Mainsail, Moonraker and your system from within Mainsail.'
---

# Update Manager

### Moonraker.conf

Add the following section to your printers moonraker.conf:

```text
[update_manager]

[update_manager client mainsail]
type: web
repo: meteyou/mainsail
path: ~/mainsail
```

Once you have restarted the moonraker service, the Update Manager will appear in Mainsails machine settings.

![](../../.gitbook/assets/update-manager.png)

{% hint style="info" %}
You can find further information on this topic by checking out the Moonraker documentation.  
[https://github.com/Arksine/moonraker/blob/master/docs/configuration.md\#update\_manager](https://github.com/Arksine/moonraker/blob/master/docs/configuration.md#update_manager)
{% endhint %}

