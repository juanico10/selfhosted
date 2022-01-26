# About

#

<p align="center">
    <a href="https://containrrr.dev/watchtower/">
        <img src="https://github.com/JuanRodenas/Docker-container-selfhosted/blob/main/watchtower/watchtower.png" alt="watchtower">
    </a>
    <br>
</p>
<!-- markdownlint-enable MD033 -->

#

Watchtower is a container-based solution for automating Docker container base image updates. It will pull down your new image, gracefully shut down your existing container and restart it with the same options that were used when it was deployed initially.

* [Github](https://github.com/containrrr/watchtower)
* [Documentation](https://containrrr.dev/watchtower/)
* [Docker Image](https://hub.docker.com/r/containrrr/watchtower)

# Usage

## Configuration

If you don't want to use gotify for the notification, feel free to remove the environnement variables from both the `.env` and the `docker-compose.yml` file.

Replace the environment variables in `.env` with your own, then run :

```bash
sudo docker-compose up -d
```

Watchtower will then check for update every monday and send you a notification with gotify once an image is updated.

# Update

The image is automatically updated with [watchtower](../watchtower) thanks to the following label :

```yaml
  # Watchtower Update
  - "com.centurylinklabs.watchtower.enable=true"
```

# Security

Automatically upgrading open-source images can be a huge security risk. The safest solution would be to only [monitor](https://containrrr.dev/watchtower/arguments/#without_updating_containers) the images and check the updated image before doing the upgrade.
