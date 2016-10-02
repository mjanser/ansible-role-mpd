# Ansible Role: mpd

An Ansible role that installs MPD (Music Player Daemon) on Fedora.

## Requirements

The UnitedRPMs or rpmfusion-free repository has to be installed before running this role.

## Role Variables

Available variables are listed below, along with default values:

    mpd_name: Music Player Daemon

    mpd_outputs:
      - name: "Null Output"
        type: "null"

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
    mpd_bind_to_address: any

    mpd_autostart: false
    mpd_firewall_zones: []

## Dependencies

None

## Example Playbook

    - hosts: all
      roles:
        - { role: mjanser.mpd }

## License

MIT
