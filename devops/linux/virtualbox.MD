1. Starting Virtual Machines During System Boot.
```
# vi /etc/default/virtualbox
VBOXAUTOSTART_DB=/etc/vbox
VBOXAUTOSTART_CONFIG=/etc/vbox/autostartvm.cfg


# vi /etc/vbox/autostartvm.cfg

default_policy = deny
root = {
    allow = true
    startup_delay = 10
}
```

vboxmanage setproperty autostartdbpath /etc/vbox/autostartvm.cfg
vboxmanage modifyvm VM1 --autostart-enabled on
# https://www.virtualbox.org/manual/ch09.html#autostart