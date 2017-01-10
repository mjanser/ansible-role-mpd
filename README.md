# Ansible Role: mpd

An Ansible role that installs MPD (Music Player Daemon) on Fedora.

## Requirements

The [UnitedRPMs](https://unitedrpms.github.io/) or [rpmfusion-free](http://rpmfusion.org/) repository has to be
installed before running this role.

For configuring the firewall the service `firewalld` has to run and the package `python-firewall` needs to be installed.

## Role Variables

Available variables are listed below, along with default values:

    mpd_outputs:
      - name: "Null Output"
        type: "null"

    mpd_name: Music Player Daemon
    mpd_restore_paused: yes
    mpd_auto_update: yes
    mpd_follow_inside_symlinks: yes
    mpd_follow_outside_symlinks: no

    mpd_music_directory: /var/lib/mpd/music
    mpd_playlist_directory: /var/lib/mpd/playlists

    mpd_db_file: /var/lib/mpd/mpd.db
    mpd_sticker_file: /var/lib/mpd/sticker.db
    mpd_state_file: /var/lib/mpd/mpdstate

    mpd_user: mpd
    mpd_autostart: false

    mpd_bind_to_address: any
    mpd_firewall_zones: []

### Outputs

The outputs for MPD can be configured with the variable `mpd_outputs`.
The properties of an output are written as is into the configuration file.
See [Configuring audio outputs](https://www.musicpd.org/doc/user/config_audio_outputs.html)
and [Output plugins](https://www.musicpd.org/doc/user/output_plugins.html) for more details.

### Configuration

There are some variables to configure the behaviour of MPD like `mpd_auto_update`, `mpd_name` and more,
see above for a complete list.

### Directories

If you want to store your music and playlists in directories other than the default ones, change the
variables `mpd_music_directory` and `mpd_playlist_directory` accordingly.
Those directories won't be created, so make sure they exist and have correct permissions set.

### Files

With the variables `mpd_db_file`, `mpd_sticker_file` and `mpd_state_file` the paths to those files can be changed.

### User

The variable `mpd_user` can be used to change the user which runs MPD. The group will also be set to this value.

### Autostart

Usually MPD will be activated using a systemd socket, so that it doesn't have to run permanetly.
You can set `mpd_autostart` to `yes` to always start MPD on boot.

### Networking

If you want that MPD only binds to a single interface, you can set that in the variable `mpd_bind_to_address`.

The variable `mpd_firewall_zones` can be used to declare firewall zones in which kodi should be accessible.
This means the port `6600/tcp` will be opened.

Currently only `firewalld` is supported which is default on Fedora.

## Dependencies

None

## Example Playbook

    - hosts: all
      roles:
        - { role: mjanser.mpd }

## License

MIT
