# Installation

## Requirements for Traefik

* [Traefik up and running](../traefik).
* A subdomain of your choice, this example uses `webdav`.
  * You should be able to create a subdomain with your DNS provider, use a `A record` with the same IP address as your root domain.

## Configuration

Replace the environment variables in `.env` with your own, then run :

```
mv sample.env .env
sed -i "s/immich.tuservidor.es/el_fqdn_que_quieras/g" .env
```

Crea un valor para `JWT_SECRET`, para ello, tienes que utilizar el siguiente comando,

```
openssl rand -base64 128
```

Mientras que si has elegido Traefik,

```
docker-compose up -d && \
docker-compose logs -f
```

