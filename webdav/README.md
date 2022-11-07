# Installation

![Docker Pulls](https://img.shields.io/docker/pulls/juanico/webdav?logo=docker&style=for-the-badge)
![Docker Image Version (latest by date)](https://img.shields.io/docker/v/juanico/webdav?logo=docker&style=for-the-badge)
![Docker Image Version (tag latest semver)](https://img.shields.io/docker/v/juanico/webdav/latest?logo=docker&style=for-the-badge)

The architectures supported by this image are:

| Architecture | Available | Tag |
| :----: | :----: | ---- |
| x86-64 | ✅ | latest |
| arm | ✅ | :arm |

## Requirements

* [Traefik up and running](../traefik).
* A subdomain of your choice, this example uses `webdav`.
  * You should be able to create a subdomain with your DNS provider, use a `A record` with the same IP address as your root domain.

## Configuration

Replace the environment variables in `.env` with your own, then run :

```bash
cp sample.env .env
htpasswd -bc htpasswd tu-usuario tu-contraseña
```

Remember to change <tu-usuario> and <tu-contraseña> for your own credentials

If you want to work with Traefik,

```
docker-compose -f docker-compose.yml -f docker-compose.traefik.yml up -d
docker-compose logs -f
```
