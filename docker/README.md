# Docker Images

This repository publishes two multi-architecture images to GitHub Container Registry:

- `ghcr.io/<owner>/<repo>/airupnp`
- `ghcr.io/<owner>/<repo>/aircast`

The images are built for `linux/amd64` and `linux/arm64` on native GitHub-hosted runners.

AirConnect needs host networking for discovery and audio serving:

```sh
docker run --rm --network host ghcr.io/<owner>/<repo>/airupnp
docker run --rm --network host ghcr.io/<owner>/<repo>/aircast
```

Additional AirConnect arguments can be passed after the image name:

```sh
docker run --rm --network host ghcr.io/<owner>/<repo>/airupnp -Z -l 1000:2000
```
