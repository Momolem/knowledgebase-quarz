---
share: true
---
## LUKS
### Setup automatic unlock:
```bash
clevis luks bind -d /dev/mmcblkp3 tpm2 '{"pcr_ids":"1,7","key":"rsa"}'
systemctl enable clevis-luks-askpass.path
dracut --regenerate-all --force
```


### Regenerate
If automatic unlock does not work anymore it needs to be regenerated. First list the used slots:
```sh
clevis luks list -d /dev/nvme0n1p3
```

Then regenerate using slot
```sh
clevis luks regen -d /dev/nvme0n1p3 -s 1
```

### Change PCRs
To change PCRs you first need to delete the key and then re-add using the wanted PCRs.
List the used slots:

```sh
clevis luks list -d /dev/nvme0n1p3
```
Remove the slot:
```sh
clevis luks unbind -d /dev/nvme0n1p3 -s 1 -f
```

Note: `-f` will not ask for confirmation but is needed if there is no other slot set up.

After that re-add the key like above.

## OBS Virtual Cam
Install v4l2loopback
```sh
sudo dnf install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm
sudo dnf install v4l2loopback 
```

```sh
git clone https://github.com/umlaeute/v4l2loopback
```