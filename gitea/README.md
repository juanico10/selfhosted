# Installation

## Requirements

* [Traefik up and running](../traefik).
* A subdomain of your choice, this example uses `bookstack`.
  * You should be able to create a subdomain with your DNS provider, use a `A record` with the same IP address as your root domain.

Recuerda abrir el puerto 2222 de tu servidor, y en el caso de que tengas router o similar, redirigir las conexiones del router a tu servidor.

El siguiente paso es levantar. Aquí solo te doy la opción de hacerlo con Traefik, porque necesitas algunas opciones que no te da la versión de caddy que estoy utilizando.

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