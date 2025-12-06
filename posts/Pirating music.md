---
tags: [article, music, technology]
title: Pirating Music
---

# Pirating Music

## Tools

YouTube-dl

youtube-dl -x --audio-format mp3 --audio-quality 0 --embed-thumbnail --add-metadata -o "%(title)s.%(ext)s" 'https://www.youtube.com/playlist?list=PLZ60rAdTLVNuCAWD8W3dZTLBXbSPda-DX'

eyeD3

https://musicbrainz.org/#:~:text=MusicBrainz%20is%20an%20open%20music,the%20data%20under%20open%20licenses.

[https://picard.musicbrainz.org/](https://picard.musicbrainz.org/)

## Downloading Music

```bash
python3 -m venv venv
	source venv/bin/activate
pip install requirements.txt
 python download.py ./downloads youtube.txt
```

## Backing up Music

```bash
# copy from pc to server
scp -r ./Youtube samfelton@192.168.1.69:~/music
```

```bash
# copy to nextcloud
sudo cp -r ./Youtube /mnt/ncdata/admin/files/Music/iPod\ music\ 2025

# files seem to have moved
sudo cp -r ~/documents/DanTarrantBirthday /var/lib/docker/volumes/nextcloud_aio_nextcloud_data/_data/admin/files/Documents/GuestRoad/
```

```bash
# assert permissions on music
sudo chmod -R 755 /mnt/ncdata/admin/files/Music/
```

```bash
# scan for files in nextcloud (can use path if files get too big)
sudo docker exec --user www-data -it nextcloud-aio-nextcloud php occ files:scan --all

# scan for music in nextcloud music app
sudo docker exec --user www-data -it nextcloud-aio-nextcloud php occ music:scan --all
```
