# About

#

<p align="center">
    <a href="https://github.com/dani-garcia/vaultwarden">
        <img src="https://github.com/JuanRodenas/Docker-container-selfhosted/tree/main/vaultwarden/bitwarden.png" alt="bitwarden">
    </a>
    <br>
</p>
<!-- markdownlint-enable MD033 -->

#

Vaultwarden is an alternative implementation of the Bitwarden server API written in Rust and compatible with upstream Bitwarden clients, it is perfect for self-hosted deployment where running the official resource-heavy service might not be ideal.

* [Github](https://github.com/dani-garcia/vaultwarden)
* [Documentation](https://github.com/dani-garcia/vaultwarden/wiki)
* [Docker Image](https://hub.docker.com/r/vaultwarden/server)

# Usage

## Requirements
- [Traefik up and running](../traefik).
- A subdomain of your choice, this example uses `vaultwarden`.
    - You should be able to create a subdomain with your DNS provider, use a `A record` with the same IP address as your root domain.

## Configuration

Replace the environment variable in `.env` with your own, then run :

```bash
sudo docker-compose up -d
```

You should then be able to access the bitwarden web-ui admin interface with the ADMIN_TOKEN. 

# Update

The image is automatically updated with [watchtower](../watchtower) thanks to the following label :

```yaml
  # Watchtower Update
  - "com.centurylinklabs.watchtower.enable=true"
```

# Security

Comment admin token to disable the admin interface after you have created your users.
The IP filtering label is set in the docker-compose, you can restrict access to this service by modifying the traefik [whitelist](traefik/rules/whitelist.yml).
