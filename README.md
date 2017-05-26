# ansible-install-mpd

Music Player Daemon main web site: http://www.musicpd.org/

This is an Ansible role to install the Music Player Daemon from source instead of via a package manager.  Some package managers may not include MP3 support, so compiling from source is needed.

NOT recommended for un-protected connection directly to the Internet, as the server is configured for access without a password.

## Requirements

If the server has a firewall enabled, it may need to be altered to allow incoming packets on TCP ports 6600 and/or 8000.  No music or playlists are included, so you'll need to supply those.  See the Role Variables section below for those locations.

## Role Variables

The defaults shown below will work "out-of-the-box" and only needs customization if they don't meet your needs.  

| Name | Description | Default Value |
| ---- | ----------- | ------------- |
| ansible_install_mpd_user | Name of the user that will own the daemon process | `mpd` |
| ansible_install_mpd_group | Group of the user that will own the daemon process | `mpd` |
| ansible_install_mpd_home | Main directory for the application to run in | `/home/mpd` |
| ansible_install_mpd_src_base | Directory to place the source code archive in | `"{{ ansible_install_mpd_home }}/src"` |
| ansible_install_mpd_url_base | Base of the URL to download the source code archive | `http://www.musicpd.org/download/mpd/0.20` |
| ansible_install_mpd_shortname | Short name of the MPD archive | `mpd-0.20.6` |
| ansible_install_mpd_filename | Full name of the MPD archive | `"{{ ansible_install_mpd_shortname }}.tar.gz"` |
| ansible_install_mpd_src | Directory to unarchive the source code in | `"{{ ansible_install_mpd_src_base }}/{{ ansible_install_mpd_shortname }}"` |
| ansible_install_mpd_executable | Fully-qualified file name of the MPD executable | `/usr/local/bin/mpd` |
| ansible_install_mpd_upstart | Fully-qualified file name of the Upstart configuration file | `/etc/init/mpd.conf` |
| ansible_install_mpd_conf | Fully-qualified file name of the MPD configuration file | `"{{ ansible_install_mpd_home }}/mpd.conf"` |
| ansible_install_mpd_music_directory | Folder to store music in | `"{{ ansible_install_mpd_home }}/music"` |
| ansible_install_mpd_playlist_directory | Folder to store playlists in | `"{{ ansible_install_mpd_home }}/playlist"` |
| ansible_install_mpd_db_file | Fully-qualified file name of the MPD database file | `"{{ ansible_install_mpd_home }}/database"` |
| ansible_install_mpd_log_file | Fully-qualified file name of the MPD log file | `"{{ ansible_install_mpd_home }}/log"` |
| ansible_install_mpd_pid_file | Fully-qualified file name of the MPD PID file | `"{{ ansible_install_mpd_home }}/pid"` |
| ansible_install_mpd_state_file | Fully-qualified file name of the MPD state file | `"{{ ansible_install_mpd_home }}/state"` |
| ansible_install_mpd_sticker_file | Fully-qualified file name of the MPD sticker file | `"{{ ansible_install_mpd_home }}/sticker.sql"` |
| ansible_install_mpd_bind_to_address | Address to bind the control interface to; examples are "any" or "localhost" | `any` |
| ansible_install_mpd_port | Address to bind the control interface to | `6600` |
| ansible_install_mpd_audio_output | Dictionary containing audio output definitions | (See **NOTE A** below) |
| ansible_install_mpd_apt_prereqs | List of APT packages to install | (See **NOTE B** below) |

**NOTE A**

Example of a HTTP stream output in the `ansible_install_mpd_audio_output` dictionary:

    httpd:
      type: httpd
      name: My HTTP Stream
      encoder: lame
      port: 8000
      bitrate: 128
      format: "44100:16:2"

**NOTE B**

List of APT packages installed as pre-requisites:
- g++-4.9
- libadplug-dev
- libao-dev
- libasound2-dev
- libaudiofile-dev
- libavahi-client-dev
- libavcodec-dev
- libavformat-dev
- libboost-dev
- libbz2-dev
- libcdio-paranoia-dev
- libcppunit-dev
- libcurl4-gnutls-dev
- libexpat-dev
- libfaad-dev
- libflac-dev
- libfluidsynth-dev
- libgme-dev
- libicu-dev
- libid3tag0-dev
- libiso9660-dev
- libjack-jackd2-dev
- libmad0-dev
- libmikmod2-dev
- libmms-dev
- libmodplug-dev
- libmp3lame-dev
- libmpcdec-dev
- libmpdclient-dev
- libmpg123-dev
- libnfs-dev
- libopenal-dev
- libopus-dev
- libpulse-dev
- libresid-builder-dev
- libroar-dev
- libsamplerate0-dev
- libshout3-dev
- libsidplay2-dev
- libsidutils-dev
- libsmbclient-dev
- libsndfile1-dev
- libsoxr-dev
- libsqlite3-dev
- libupnp-dev
- libvorbis-dev
- libwavpack-dev
- libwildmidi-dev
- libwrap0-dev
- libyajl-dev
- libzzip-dev
- xmlto

## Dependencies

This role depends on no other roles.  

## Example Playbook

Configure a MPD server for localhost access only:

    - hosts: servers
      roles:
         - { role: kso512.ansible-install-mpd, ansible_install_mpd_bind_to_address: 127.0.0.1 }

## License

BSD

## Author Information

> Chris Lindbergh @kso512
