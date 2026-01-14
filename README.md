# Hytale Server Docker Image

**An unofficial Docker image for containerized Hytale servers.**

## Download

- **Docker Hub**: [jirisitera/hytale-server](https://hub.docker.com/r/jirisitera/hytale-server)
- **Alternative (GHCR)**: [ghcr.io/jirisitera/docker-hytale-server](https://ghcr.io/jirisitera/docker-hytale-server)

## Features

- automatic downloading of server files
- configurable by environment variables

## Quickstart

You can use the following [compose.yml](compose.yml) as a starting point:

```yaml
name: hytale
services:
  hytale:
    container_name: hytale
    image: hytale
    build: .
    restart: on-failure:3
    stdin_open: true
    tty: true
    networks:
      - hytale
    volumes:
      - hytale:/data
    ports:
      - "5520:5520/udp"
    environment:
      HYTALE_AUTO_DOWNLOAD: "true"
networks:
  hytale:
    name: hytale
volumes:
  hytale:
    name: hytale
```

Then run:

```bash
docker compose up -d
```

> [!IMPORTANT]
> **These steps are required for proper setup:**
>
> 1. **Downloader authentication** (first run): click the URL and device code in the logs to download server files
> 2. **Server authentication** (after startup): attach to the console (`docker compose attach hytale`), then run `/auth persistence Encrypted` followed by `/auth login device`

## Java Version

Hytale requires Java 25. This image uses Eclipse Temurin by Adoptium, which is recommended by the Hytale team.

## Contributing & Security

- see [CONTRIBUTING.md](CONTRIBUTING.md)
- see [SECURITY.md](SECURITY.md)

## License

This project is not at all affiliated with Hypixel Studios or Hytale.

Proudly licensed under the [MIT LICENSE](LICENSE.txt).
