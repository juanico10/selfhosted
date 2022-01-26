# About

<p align="center">
<img src="../_utilities/gotify.png" width="400" alt="gotify" title="gotify" />
</p>

Gotify is a simple server for sending and receiving notification messages. It is used a lot throughout this guide for services such as backups and automatic updates, a must-have self-hosted solution.

* [Github](https://github.com/gotify/server)
* [Documentation](https://gotify.net/docs/index)
* [Docker Image](https://hub.docker.com/r/gotify/server)

# Usage

## Requirements
- [Traefik up and running](../traefik).
- A subdomain of your choice, this example uses `gotify`.
    - You should be able to create a subdomain with your DNS provider, use a `A record` with the same IP address as your root domain.

## Configuration

Replace the environment variables in `.env` with your own, then run :

```bash
sudo docker-compose up -d
```

You should then be able to access the gotify web-ui with the default user being `admin` and the GOTIFY_DEFAULTUSER_PASS defined in `.env`.

# Update

The image is automatically updated with [watchtower](../watchtower) thanks to the following label :

```yaml
  # Watchtower Update
  - "com.centurylinklabs.watchtower.enable=true"
```