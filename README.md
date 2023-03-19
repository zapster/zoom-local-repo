# zoom-local-repo
Maintain a local RPM repository for the zoom client

* check if `https://zoom.us/client/latest/zoom_x86_64.rpm` points to a new version
* download new version
* update local repository

## Requirements

* `wget`
* `createrepo`

## Installation


### Install systemd user files
```
cd ~/.config/systemd/user/
ln -s path/to/zoom-local-repo/zoom-local.service
ln -s path/to/zoom-local-repo/zoom-local.timer
systemctl --user enable zoom-local.timer
systemctl --user start zoom-local.timer
systemctl --user list-timers
```

### Install Local dnf Respository
Install Zoom GPG key. https://zoom.us/linux/download/pubkey?version=5-12-6
```
sudo rpm --import https://zoom.us/linux/download/pubkey?version=5-12-6
sudo dnf config-manager --add-repo zoom-local.repo
repoquery -a --repoid=zoom-local
```
