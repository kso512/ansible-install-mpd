# [ansible-install-mpd](https://galaxy.ansible.com/kso512/ansible-install-mpd/)

[![Build Status](https://travis-ci.org/kso512/ansible-install-mpd.svg?branch=master)](https://travis-ci.org/kso512/ansible-install-mpd) ![Ansible Role](https://img.shields.io/ansible/role/d/16931) [![made-with-bash](https://img.shields.io/badge/Made%20with-Bash-1f425f.svg)](https://www.gnu.org/software/bash/) [![made-with-Markdown](https://img.shields.io/badge/Made%20with-Markdown-1f425f.svg)](http://commonmark.org) ![GitHub](https://img.shields.io/github/license/kso512/ansible-install-mpd)

[![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/kso512/ansible-install-mpd)](https://github.com/kso512/ansible-install-mpd) ![GitHub Release Date](https://img.shields.io/github/release-date/kso512/ansible-install-mpd) ![GitHub repo size](https://img.shields.io/github/repo-size/kso512/ansible-install-mpd) ![GitHub issues](https://img.shields.io/github/issues-raw/kso512/ansible-install-mpd) [![GitHub forks](https://img.shields.io/github/forks/Naereen/StrapDown.js.svg?style=social&label=Fork&maxAge=2592000)](https://GitHub.com/Naereen/StrapDown.js/network/)

An [Ansible](https://www.ansible.com/) [Role](http://docs.ansible.com/ansible/playbooks_roles.html#roles) to install the [Music Player Daemon](http://www.musicpd.org/) application from source instead of via a package manager.  Some package managers may not include features such as MP3 support, so compiling from the source code may help.

**I do not recommend the default configuration for unprotected connection directly to the Internet, as the server configuration includes access without a password.**  Instead, I recommend the operator increase security by configuring a host or group variable that overrides `ansible_install_mpd_conf_src` with a custom file from outside the repository.

Tested with [Travis continuous integration](https://travis-ci.org/) on the following distributions:

- [Debian 10 "Buster"](https://www.debian.org/releases/buster/)
- [Ubuntu 18.04 LTS "Bionic Beaver"](http://releases.ubuntu.com/18.04/)

## Requirements

If the server has a firewall enabled, it may need alteration to allow incoming packets on TCP ports 6600/8000.  The role includes no music or playlists, so you'll need to supply those.  See the [Role Variables](https://github.com/kso512/ansible-install-mpd#role-variables) section below for those locations.

## Role Variables

The default values shown below should work "out-of-the-box" and only need customization if they don't meet your needs.

| Name | Description | Default Value |
| ---- | ----------- | ------------- |
| ansible_install_mpd_apt_prereqs | List of APT packages to install | (See [NOTE A](https://github.com/kso512/ansible-install-mpd#note-a) below) |
| ansible_install_mpd_audio_output | Dictionary containing audio output definitions | (See [NOTE B](https://github.com/kso512/ansible-install-mpd#note-b) below) |
| ansible_install_mpd_bind_to_address | Address to bind the control interface to; examples are "any" or "localhost" | `any` |
| ansible_install_mpd_conf | Fully-qualified file name of the MPD configuration file | `{{ ansible_install_mpd_home }}/mpd.conf` |
| ansible_install_mpd_conf_src | Relative or fully-qualified file name of the MPD configuration file source | `mpd.conf.j2` |
| ansible_install_mpd_db_file | Fully-qualified file name of the MPD database file | `{{ ansible_install_mpd_home }}/database` |
| ansible_install_mpd_executable | Fully-qualified file name of the MPD executable | `/usr/local/bin/mpd` |
| ansible_install_mpd_filename | Full name of the MPD archive | `{{ ansible_install_mpd_shortname }}.tar.gz` |
| ansible_install_mpd_gcc_version | Version of the Gnu C Compiler to install | (See [NOTE C](https://github.com/kso512/ansible-install-mpd#note-c) below) |
| ansible_install_mpd_group | Group of the user that will own the daemon process | `mpd` |
| ansible_install_mpd_home | Main directory for the application to run in | `/home/mpd` |
| ansible_install_mpd_log_file | Fully-qualified file name of the MPD log file | `{{ ansible_install_mpd_home }}/log` |
| ansible_install_mpd_music_directory | Folder to store music in | `{{ ansible_install_mpd_home }}/music` |
| ansible_install_mpd_pid_file | Fully-qualified file name of the MPD PID file | `{{ ansible_install_mpd_home }}/pid` |
| ansible_install_mpd_playlist_directory | Folder to store playlists in | `{{ ansible_install_mpd_home }}/playlist` |
| ansible_install_mpd_port | Address to bind the control interface to | `6600` |
| ansible_install_mpd_shortname | Short name of the MPD archive | `mpd-0.21.21` |
| ansible_install_mpd_src | Directory to unarchive the source code in | `{{ ansible_install_mpd_src_base }}/{{ ansible_install_mpd_shortname }}` |
| ansible_install_mpd_src_base | Directory to place the source code archive in | `{{ ansible_install_mpd_home }}/src` |
| ansible_install_mpd_state_file | Fully-qualified file name of the MPD state file | `{{ ansible_install_mpd_home }}/state` |
| ansible_install_mpd_sticker_file | Fully-qualified file name of the MPD sticker file | `{{ ansible_install_mpd_home }}/sticker.sql` |
| ansible_install_mpd_systemd_service_dest | Fully-qualified file name of the MPD systemd service unit file | `/lib/systemd/system/mpd.service` |
| ansible_install_mpd_systemd_service_src | Relative or fully-qualified file name of the MPD systemd service unit file source | `systemd.mpd.service.j2` |
| ansible_install_mpd_systemd_socket_dest | Fully-qualified file name of the MPD systemd socket unit file | `/lib/systemd/system/mpd.socket` |
| ansible_install_mpd_systemd_socket_src | Relative or fully-qualified file name of the MPD systemd socket unit file source | `systemd.mpd.socket.j2` |
| ansible_install_mpd_url_base | Base of the URL to download the source code archive | `http://www.musicpd.org/download/mpd/0.21` |
| ansible_install_mpd_user | Name of the user that will own the daemon process | `mpd` |

### NOTE A

List of APT packages installed as pre-requisites:

- cmake
- libadplug-dev
- libao-dev
- libasound2-dev
- libaudio-mpd-perl
- libaudiofile-dev
- libavahi-client-dev
- libavcodec-dev
- libavformat-dev
- libboost-all-dev
- libbz2-dev
- libcdio-paranoia-dev
- libcppunit-dev
- libcurl4-gnutls-dev
- libexpat-dev
- libfaad-dev
- libflac-dev
- libfluidsynth-dev
- libgme-dev
- libgtest-dev
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
- libpcre3-dev
- libpulse-dev
- libresid-builder-dev
- libroar-dev
- libsamplerate0-dev
- libshout3-dev
- libsidplay2-dev
- libsidutils-dev
- libsmbclient
- libsmbclient-dev
- libsndfile1-dev
- libsndio-dev
- libsoxr-dev
- libsqlite3-dev
- libsystemd-dev
- libtwolame-dev
- libupnp-dev
- libvorbis-dev
- libwavpack-dev
- libwildmidi-dev
- libwrap0-dev
- libyajl-dev
- libzzip-dev
- ninja-build
- python3
- python3-pip
- unzip
- xmlto

### NOTE B

Example of a HTTP stream output in the `ansible_install_mpd_audio_output` dictionary:

    httpd:
      type: httpd
      name: My HTTP Stream
      encoder: lame
      port: 8000
      bitrate: 128
      format: "44100:16:2"

### NOTE C

This role utilizes [`include_vars` and `with_first_found`](http://docs.ansible.com/ansible/include_vars_module.html) with the `ansible_install_mpd_gcc_version` variable to specify which version of the Gnu C Compiler to install.

- Debian systems default to `6` until Debian 10 "Buster" using `7`.
- Ubuntu systems default to `6`.

## Dependencies

This role depends on none other.

## Example Playbook

Configure each MPD server for localhost access only and a custom mpd.conf:

    - hosts: servers
      roles:
        - { role: kso512.ansible-install-mpd, ansible_install_mpd_bind_to_address: 127.0.0.1, ansible_install_mpd_conf_src: local/mpd.conf.j2 }

## License

[GNU General Public License version 2](https://www.gnu.org/licenses/gpl-2.0.txt)

## Author Information

> Chris Lindbergh @kso512
