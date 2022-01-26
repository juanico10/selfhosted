# About

#

<p align="center">
    <a href="https://github.com/zadam/trilium/wiki/">
        <img src="https://github.com/JuanRodenas/Docker-container-selfhosted/blob/main/trilium/trilium.png" alt="trilium">
    </a>
    <br>
</p>
<!-- markdownlint-enable MD033 -->

#

Trilium Notes is a hierarchical note-taking application with focus on building large personal knowledge bases

* [Github](https://github.com/zadam/trilium)
* [Documentation](https://github.com/zadam/trilium/wiki/)
* [Docker Image](https://hub.docker.com/r/zadam/trilium)

# Usage

## Requirements

* [Traefik up and running](../traefik).
* A subdomain of your choice, this example uses `trilium`.
  * You should be able to create a subdomain with your DNS provider, use a `A record` with the same IP address as your root domain.

## Configuration

Replace the environment variables in `.env` with your own, then run :

```bash
sudo docker-compose up -d
```

You should then be able to access the trilium web-ui and start creating notes !

# Update

The image is automatically updated with [watchtower](../watchtower) thanks to the following label :

```yaml
  # Watchtower Update
  - "com.centurylinklabs.watchtower.enable=true"
```
