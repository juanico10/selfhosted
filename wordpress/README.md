# About

<p align="center">
<img src="../_utilities/wordpress.png" width="400" alt="wordpress" title="wordpress" />
</p>

WordPress is a free and open source blogging tool and a content management system (CMS) based on PHP and MySQL, which runs on a web hosting service.

* [Github](https://github.com/WordPress/WordPress)
* [Documentation](https://codex.wordpress.org/)
* [Docker Image](https://hub.docker.com/_/wordpress)

# Usage

## Requirements
- [Traefik up and running](../traefik).
- A subdomain of your choice, this example uses `wordpress`.
    - You should be able to create a subdomain with your DNS provider, use a `A record` with the same IP address as your root domain.

## Configuration

Replace the environment variables in `.env` with your own.

Then replace the following variables in `data/wp-config.php`.

* DB_PASSWORD is equivalent to DB_PASSWD in `.env`
  ```
  define( 'DB_PASSWORD', 'xxxxxxxxxxxxxxx' );
  ```

* Change the following unique keys and salt, you can use this [wordpress salt generator](https://api.wordpress.org/secret-key/1.1/salt/) and copy past it
  ```
  define( 'AUTH_KEY',         'change-me' );
  define( 'SECURE_AUTH_KEY',  'change-me' );
  define( 'LOGGED_IN_KEY',    'change-me' );
  define( 'NONCE_KEY',        'change-me' );
  define( 'AUTH_SALT',        'change-me' );
  define( 'SECURE_AUTH_SALT', 'change-me' );
  define( 'LOGGED_IN_SALT',   'change-me' );
  define( 'NONCE_SALT',       'change-me' );
  ```

You can now run :

```bash
sudo docker-compose up -d
```

You should now be able to access the wordpress initialisation page.

# Update

The image is automatically updated with [watchtower](../watchtower) thanks to the following label :

```yaml
  # Watchtower Update
  - "com.centurylinklabs.watchtower.enable=true"
```
ACCESS_DENIED\