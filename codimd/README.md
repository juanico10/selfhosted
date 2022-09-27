# Installation

## Requirements

* [Traefik up and running](../traefik).
* A subdomain of your choice, this example uses `codimd`.
  * You should be able to create a subdomain with your DNS provider, use a `A record` with the same IP address as your root domain.

## Configuration

Replace the environment variables in `.env` with your own, then run :

```bash
sudo docker-compose up -d
```

You should now be able to access the codimd setup instruction, it is quite straigthforward and nothing is required. 

# Update

The image is automatically updated with [watchtower](../watchtower) thanks to the following label :

```yaml
  # Watchtower Update
  - "com.centurylinklabs.watchtower.enable=true"
```