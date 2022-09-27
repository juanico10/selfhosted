# Installation

## Requirements

* [Traefik up and running](../traefik).
* A subdomain of your choice, this example uses `bookstack`.
  * You should be able to create a subdomain with your DNS provider, use a `A record` with the same IP address as your root domain.

* Port default
```bash
  bookstack:
    ports:
      - 8080:80
```

## Configuration

Replace the environment variables in `.env` with your own, then run :

```bash
sudo docker-compose up -d
```

You should now be able to access the bookstack setup instruction, it is quite straigthforward and nothing is required. 

# Update

The image is automatically updated with [watchtower](../watchtower) thanks to the following label :

```yaml
  # Watchtower Update
  - "com.centurylinklabs.watchtower.enable=true"
```

Default credentials:

  * username: admin@admin.com
  * password: password
