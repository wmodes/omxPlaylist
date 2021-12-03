# omxPlaylist
## About
This project is designed to provide a mechanism for playing groups of media files (a directory of files) in sequence (a playlist) using Python and [OMXPlayer](https://github.com/popcornmix/omxplayer). It is meant to be used on a Raspberry PI running Debian Linux.

Also provided is the ability to use `systemd` to auto-boot the playlist and install/uninstall scripts to make the setup easy.

A secondary intention of this project is to provide a simple example of how to setup a Raspberry PI for use as a simple service provider (a media player). The files contained in this repo should be easy enough to modify in order to create any other type of service (e.g. DHCP server, MongoDB, APACHE web server).

This is a fork of [omxPlaylist](https://github.com/sabjorn/omxPlaylist) with added loop and random options.

## Usage
This project used `systemd` to start `omxPlaylist.py` at startup. However, if the `install` script is not used, `omxPlaylist.py` can be run directly with:

```
python3 omxPlaylist.py [media_dir]
```

### Options

```
usage: omxPlaylist.py [-h] [-l] [-r] [-d] ARG ...

Plays all of the media files in a directory with omxplayer.

positional arguments:
  ARG           pass ARG to the program
  remaining     catch all other arguments to be passed to OMXplayer

optional arguments:
  -h, --help    show this help message and exit
  -l, --loop    loop the playlist
  -r, --random  play playlist in random order
  -d, --debug   increase output verbosity
```

### Install
To `install`, run:

```
chmod u+x install.sh
sudo ./install.sh
```

### Uninstall
To `uninstall`, run:

```
chmod u+x install.sh
sudo ./uninstall.sh
```

Importantly, the `omxPlaylist.service` (`systemd` service which runs the script at boot) is hardcoded to use the `/media/omxPlaylist` directory as the source for media files. Media can be copied or symlinked to this directory to play. Alternatively, `systemd/omxPlaylist.service` can be modified, replacing:

```
/media/omxPlaylist
```

with whichever directory you wish to have your media. Then, re-run the `install.sh` script.

**Note**: For both `install.sh` and `uninstall.sh`, the `chmod` command is only required once.
