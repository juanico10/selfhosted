# About

#

<p align="center">
    <a href="https://transmissionbt.com/">
        <img src="https://github.com/JuanRodenas/Docker-container-selfhosted/tree/main/transmission/transmission.png" alt="transmission">
    </a>
    <br>
</p>
<!-- markdownlint-enable MD033 -->

#

Transmission is a fast, easy, and free BitTorrent client.

* [Github](https://github.com/transmission/transmission)
* [website](https://transmissionbt.com/)
* [Docker Image](https://hub.docker.com/r/linuxserver/transmission)

# Usage

## Requirements

* [Traefik up and running](../traefik).
* A subdomain of your choice, this example uses `transmission`.
  * You should be able to create a subdomain with your DNS provider, use a `A record` with the same IP address as your root domain.
* Port 51413 open, check your firewall.

## Configuration

The linuxserver images are using the PUID and PGID, they allow the container to map the container's internal user to a user on the host machine, more information [here](https://docs.linuxserver.io/general/understanding-puid-and-pgid).

To find yours, use `id user`. Replace the environment variables in `.env` with your own, then run :

```bash
sudo docker-compose up -d
```

# Update

The image is automatically updated with [watchtower](../watchtower) thanks to the following label :

```yaml
  # Watchtower Update
  - "com.centurylinklabs.watchtower.enable=true"
```
