# Snibox
Gestor de fragmentos de código auto-alojado. Desarrollado para recoger y organizar fragmentos de código utilizando Sqlite como base de datos.

```

## Usage
* Realiza un pull con la imagen: 
`docker pull melashri/snibox:latest`

* Docker compose:
```bash
---
version: '3.7'

services:
  nginx-puma:
    container_name: snibox-nginx
    image: juanico/nginx-puma:snibox
    init: true
    restart: unless-stopped
    volumes:
      - './static-files:/var/www/html'
    depends_on:
      - backend
    ports:
        - '80:80'

  backend:
    container_name: snibox-backend
    image: juanico/snibox:latest
    init: true
    volumes:
        - './data/app/db:/app/db/database'
    restart: unless-stopped
    env_file:
        - .env
    depends_on:
      - backend-cache

  backend-cache:
    image: redis:alpine
    container_name: snibox-redis
    healthcheck:
      test: redis-cli ping
      interval: 10s
      timeout: 5s
      retries: 5
    restart: unless-stopped
```
El contenedor ejecuta `rake db:migrate` en cada inicio, para crear el archivo de la base de datos si no existe, o actualizar el esquema de la base de datos si es necesario, por lo que las copias de seguridad son muy recomendables.

### Environment variables
`DATABASE` - Define la ubicación del archivo de la base de datos sqlite3 dentro del contenedor.

_Default_: `/app/db/database/snibox.sqlite3`

---

`SECRET_KEY_BASE` - Define el parámetro `secret_key_base` para tu aplicación Rails. El parámetro por defecto ya está incluido en la imagen, pero la recomendación general es cambiarlo.

---

`LOGLEVEL` - Define el nivel de registro de la aplicación Rails. Las opciones disponibles son: `debug`, `info`, `warn`, `error` and `fatal`
_Default_: `debug`
