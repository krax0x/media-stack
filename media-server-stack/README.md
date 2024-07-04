# Media Server Docker Compose Configuration

This Docker Compose configuration sets up a comprehensive media server stack, including media management, torrent downloading, subtitle management, and automatic updates, all within Docker containers.
 
 > [!warning] 
 > Only for educational purposes!

## Prerequisites

Before running this setup, ensure you have the following installed on your host machine:

- Docker
- Docker Compose (version 3.9)
## Configuration

Ensure you have the following directory structure on your host machine:
```arduino
data
├── config 
├── downloads 
│   ├── movies 
│   ├── music 
│   ├── tv 
└── media
    ├── movies
    ├── music
    └── tv
```

Replace `${BASE_DIR}`, `${CONFIG_DIR}`, `${MEDIA_DIR}`, `${DOWNLOAD_DIR}` with appropriate paths according to your setup in .env file.
## Getting Started

1. Clone this repository to your local machine.
2. Update the `.env` file with appropriate values for `PUID`, `PGID`, and `TIMEZONE`.
3. Customize the paths in the Docker Compose file (`docker-compose.yml`) according to your setup.
4. Run `docker-compose up -d` to start all services in detached mode.

 > [!note]
 >  - Ensure the specified ports are available and not used by other services.
 >  - Adjust the configuration and volumes as needed based on your specific requirements.
 >  - Refer to the respective documentation for each service for more detailed configuration options and troubleshooting.
 
 ## Services

### Jellyfin

[Jellyfin](https://jellyfin.org/) is a free, open-source media server that enables you to organize, stream, and share your media.

- **Port:** 8096
- **Volumes:** `${CONFIG_DIR}/jellyfin:/cache`, `${CONFIG_DIR}/jellyfin:/config`, `${MEDIA_DIR}:/data/media`

### qBittorrent

[qBittorrent](https://www.qbittorrent.org/) is a fast, lightweight torrent client with a web interface.

- **Port:** 8080
- **Volumes:** `${CONFIG_DIR}/qbittorrent:/config`, `${DOWNLOAD_DIR}:/data/downloads`. 

### Prowlarr

[Prowlarr](https://github.com/Prowlarr/Prowlarr) is an indexer that allows you to use torrent trackers with *arr services.

- **Port:** 9696
- **Volumes:** `${CONFIG_DIR}/prowlarr:/config`

### Sonarr

[Sonarr](https://sonarr.tv/) is a tv show collection manager for Usenet and BitTorrent users.

- **Port:** 8989
- **Volumes:** `${CONFIG_DIR}/sonarr:/config`, `${BASE_DIR}:/data`

### Radarr

[Radarr](https://radarr.video/) is a movie collection manager for Usenet and BitTorrent users.

- **Port:** 7878
- **Volumes:** `${CONFIG_DIR}/radarr:/config`, `${BASE_DIR}:/data`

### Bazarr

[Bazarr](https://www.bazarr.media/) is a companion application to Sonarr and Radarr that manages and downloads subtitles.

- **Port:** 6767
- **Volumes:** `${CONFIG_DIR}/bazarr:/config`, `${MEDIA_DIR}:/data/movies`

### WatchTower

[Watchtower](https://containrrr.dev/watchtower/) automatically updates Docker containers when new versions are available.

- **Volumes:** `/var/run/docker.sock:/var/run/docker.sock`

### Jellyseerr

[Jellyseerr](https://github.com/fallenbagel/Jellyseerr) is a service for managing requests for movies and shows.

- **Port:** 5055
- **Volumes:** `${CONFIG_DIR}/jellyseerr:/config`

## Useful links

- Amazing repo with plugins for jellyfin - [Awesome Jellyfin](https://github.com/awesome-jellyfin/awesome-jellyfin?tab=readme-ov-file)
