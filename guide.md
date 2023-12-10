# Table of Contents

- Docker (
  [Install](https://bytexd.com/how-to-install-docker-on-rhel) /
  [Uninstall](https://stackoverflow.com/questions/48962730/docker-not-completely-removed)
  )
- Pm2 (
  [Install](https://pm2.keymetrics.io/docs/usage/quick-start) /
  [Share the same daemon process](https://sobus-piotr.medium.com/pm2-share-the-same-daemon-process-between-multiple-users-dd7ecae6197a)
  )
- Pyenv ( [Install](https://blog.teclado.com/how-to-use-pyenv-manage-python-versions) )
- [Update chrome](#update-chrome)
- [Create web shortcut on desktop](#create-web-shortcut-on-desktop)
- [How to connect docker container database in localhost](https://stackoverflow.com/a/62741987)
- [Bypass capcha v2](https://www.youtube.com/watch?v=Fdu81T9GgMA&ab_channel=OhYicong)
- [Connect to multi databases in NodeJS](https://school.geekwall.in/p/H1gUJiuDN)
- [Face recognition with Python](https://www.youtube.com/watch?v=tl2eEBFEHqM&ab_channel=Indently)

## Update chrome

```bash
sudo apt update
sudo apt upgrade google-chrome-stable
```

## Create web shortcut on desktop

Create new file ${SHORTCUT_NAME}.desktop

```bash
# https://askubuntu.com/a/1296032
[Desktop Entry]
Name=${NAME}
Comment=""
Exec=google-chrome-stable ${LINK}
Icon=/path-icon.png
# create shortcut from the web to get the icon
Icon=chrome-eilembjdkfgodjkcjnpgpaenohkicgjd-Default # or local path
Terminal=false
Type=Application
```

Then right click on the gear icon, select "Allow Launching" and move this file to

```bash
/usr/share/applications (global - required)
~/.local/share/applications (local - optional)
```

---
