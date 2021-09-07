# Home Assistant Add-on: Remote Backup

The addon transfers the changes to the destination every time the addon is started. After the transfer, the addon stops.

It has a `scp` and `rsync` function -- with the ability to transfer [HassOS](https://github.com/home-assistant/operating-system) folders (`/addons`, `/backup`, `/config`, `/share`, `/ssl` and `/media`) to a remote `rsync` or `ssh` server (*e.g. a Synology NAS*).

You might want to start the transfer with an automation in Home Assistant. For example:
```
- id: '7'
  alias: Create backup & Folder sync to NAS
  trigger:
    platform: time
    at: '1:00:00'
  action:
  - service: hassio.addon_start
    data:
      addon: 36883ed7_remote_backup
```

## Installation

Adding this add-ons repository to your Hass.io Home Assistant instance is
pretty easy. Follow https://home-assistant.io/hassio/installing_third_party_addons/ on the
website of Home Assistant, and use the following URL:

```
https://github.com/blizzrdof77/hassio-addons
```

## Configuration

**Note**: _Remember to restart the add-on when the configuration is changed._

Example add-on configuration:

```yaml
ssh_enabled: true
ssh_host: mynas.local
ssh_port: 22
ssh_user: johnnybackup
ssh_key:
  - '-----BEGIN OPENSSH PRIVATE KEY-----'
  - abcdefghijklmnopqrstuvwxyz01234567891011121314151617181920212223242526
  - abcdefghijklmnopqrstuvwxyz01234567891011121314151617181920212223242526
  - abcdefghijklmnopqrstuvwxyz01234567891011121314151617181920212223242526
  - abcdefghijklmnopqrstuvwxyz01234567891011121314151617181920212223242526
  - abcdefghijklmnopqrstuvwxyz012345678910111213==
  - '-----END OPENSSH PRIVATE KEY-----'
remote_directory: /volumes/Backups/HassOS
zip_password: ''
keep_local_backup: 5
rsync_enabled: false
rsync_host: ''
rsync_rootfolder: hassio-sync
rsync_user: ''
rsync_password: ''
```

**Note**: _This is just an example, don't copy and paste it! Create your own!_

### Option: `ssh_enabled`

Whether or not to use `ssh` (`scp`) to transfer the completed backup to 
a remote server.

### Option: `ssh_host`

The host or IP address of the remote `SSH` server.

### Option: `ssh_port`

The port to use when connecting via `ssh`.

### Option: `ssh_user`

The username to use when connecting via `ssh`.

### Option: `ssh_key`

The private key (*formated as a YAML list* -- *see example configuration above*) to use when connecting via `ssh`.

### Option: `remote_directory`

The full path of the directory on the remote server to which your completed backup archive will be copied. 

### Option: `zip_password`

Optionally provide a password to protect the completed backups.

### Option: `keep_local_backup`

The number (`integer`) of backups to keep locally (*older backups will be removed automatically*).

### Option: `rsync_enabled`

Whether or not to use `rsync` to transfer the completed backup to 
a remote `rsync` server.

### Option: `rsync_host`

The host or IP address of the remote `SSH` server.

### Option: `rsync_rootfolder`

The full path of the root `rsync` directory. 

### Option: `rsync_user`

The username to use when connecting via `rsync`.

### Option: `rsync_password`

The password to use when connecting via `rsync`.

## Known issues and limitations

- This add-on requires an accessible remote server with either `ssh` or `rsync` installed.

## Authors & contributors

This addon is a fork of the great backup addon [hassio-remote-backup](https://github.com/overkill32/hassio-remote-backup) by [@overkill32](https://github.com/overkill32), which *creates and manages* ***backups*** (formerly called **snapshots**). 

For a full list of all authors and contributors, check [the contributor's page](https://github.com/carstenschroeder/hassio-addons/graphs/contributors).

## License

MIT License

Copyright (c) 2019 carstenschroeder

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

[contributors]: https://github.com/carstenschroeder/hassio-addons/graphs/contributors
[discord-ha]: https://discord.gg/c5DvZ4e
[reddit]: https://reddit.com/r/homeassistant
