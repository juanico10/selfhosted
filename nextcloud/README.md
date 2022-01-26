# About

<p align="center">
<img src="../_utilities/nextcloud.png" width="400" alt="nextcloud" title="nextcloud" />
</p>

Nextcloud is a safe home for all your data. Access & share your files, calendars, contacts, mail & more from any device, on your terms.

* [Github](https://github.com/nextcloud/docker)
* [Documentation](https://docs.nextcloud.com/server/latest/admin_manual/contents.html)
* [Docker Image](https://hub.docker.com/_/nextcloud)

# Usage

## Requirements
- [Traefik up and running](../traefik).
- A subdomain of your choice, this example uses `nextcloud`.
    - You should be able to create a subdomain with your DNS provider, use a `A record` with the same IP address as your root domain.

## Configuration

Replace the environment variables in `.env` with your own, then run :

```bash
sudo docker-compose up -d
```

You should now be able to access the nextcloud admin account creation. 
Nextcloud will ask you to create your admin account as well as to choose what type of database your want to use. In the docker-compose we set up a mariadb database, choose it and enter the following database credentials.

<p align="center">
<img src="../_utilities/nextcloud_instruction.png" width="250" alt="nextcloud_instruction" title="nextcloud_instruction" />
</p>

The password is the one you have modified in the `.env` file : DB_PASSWD.
Nextcloud will now finish installing and will soon be ready to use.


# Update

The image is automatically updated with [watchtower](../watchtower) thanks to the following label :

```yaml
  # Watchtower Update
  - "com.centurylinklabs.watchtower.enable=true"
```

# Security

Nextcloud provides client-side end-to-end data encryption. You can create encrypted libraries to use this feature. Use this feature to add extra security to your documents.