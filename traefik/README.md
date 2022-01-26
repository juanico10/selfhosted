# About

#

<p align="center">
    <a href="https://traefik.io/">
        <img src="https://github.com/JuanRodenas/Docker-container-selfhosted/blob/main/traefik/traefik.logo.png" alt="traefik">
    </a>
    <br>
</p>
<!-- markdownlint-enable MD033 -->

#

Traefik is a modern HTTP reverse proxy and load balancer that makes deploying microservices easy. 
It is an Edge Router, it means that it's the door to your platform, and that it intercepts and routes every incoming request.

* [Github](https://github.com/traefik/traefik/)
* [Documentation](https://doc.traefik.io/traefik/)
* [Docker Image](https://hub.docker.com/_/traefik)

Traefik is a key component for this selfhosted infrastructure, it is providing the following features :

- Act as a reverse proxy, enabling you to self-hosted multiple services behind a single IP
- HTTPS for your services by leveraging Let's Encrypt
- Easily configure TLS for all services
- Use a whitelist to restrict services to a fix set of IPs

The docker-compose contains two services :
- socket-proxy : This ensures Docker’s socket file to not be exposed to the public
- traefik : Traefik application configuration

## socket-proxy

The socket-proxy service is used to protect the docker socket, allowing Traefik unrestricted access to your Docker socket file could result in a vulnerability to the host computer, as per [Traefik own documentation](https://doc.traefik.io/traefik/providers/docker/#docker-api-access), should any other part of the Traefik container ever be compromised. 

Instead of allowing Traefik container full access to the Docker socket file, we can instead proxy only the API calls we need with [Tecnativa’s Docker Socket Proxy](https://github.com/Tecnativa/docker-socket-proxy), following the [principle of the least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).

## traefik

### DNS Challenge with Let's Encrypt

Traefik can use an ACME provider (like Let's Encrypt) for automatic certificate generation. It will create the certificate and attempt to renew it automatically 30 days before expiration. One of the great benefit of using DNS challenges is that it will allow us to use wildcard certificates, on the other hand, it can create a security risk as it requires giving rights to Traefik to create and remove some DNS records.

For the DNS challenge, you'll need a [working provider](https://doc.traefik.io/traefik/https/acme/#providers) along with the credentials allowing to create and remove DNS records, 
If you are using OVH, you can use this [guide](https://medium.com/nephely/configure-traefik-for-the-dns-01-challenge-with-ovh-as-dns-provider-c737670c0434) to retrieve the credentials.


### Global redirect to HTTPS

```yaml
      # global redirect to https
      - "traefik.http.routers.http-catchall.rule=hostregexp(`{host:.+}`)"
      - "traefik.http.routers.http-catchall.entrypoints=http"
      - "traefik.http.routers.http-catchall.middlewares=redirect-to-https"
```
This rule will match all the HTTP requests and redirect them to HTTPS. It uses the redirect-to-https middleware.

### Redirect root to www

```yaml
      # redirect root to www
      - "traefik.http.routers.root.rule=host(`example.com`)"
      - "traefik.http.routers.root.entrypoints=https"
      - "traefik.http.routers.root.middlewares=redirect-root-to-www"
      - "traefik.http.routers.root.tls=true"
```
This rule will automatically redirect the root domain `example.com` to `www.example.com`. You can use the [webserver](../webserver) example to set up a website using docker. 

# Usage

## Requirements
- A domain, we will use example.com for this guide.
- DNS manager, usually it goes with the provider you used for your domain. We will use OVH for the guide. List of compatible [providers](https://doc.traefik.io/traefik/https/acme/#providers).
- Ports 80 and 443 open, check your firewall.


## Configuration
Before using the docker-compose file, please update the following configurations.

- **change the domain** : The current domain is example.com, change it to your domain. The change need to be made in `.env` and `traefik.yml` <br>
  ```bash
    DOMAIN=example
    TLD=com
    sed -i -e "s/example/'$DOMAIN'/g" .env 
    sed -i -e "s/com/'$TLD'/g" .env
    sed -i -e "s/example.com/'$DOMAIN'.'$TLD'/g" traefik.yml 
  ```
  
- **change the dns provider credentials** : Replace the provider name in `traefik.yml` if you are not using ovh. Replace the environment variables in `.env` and in `docker-compose.yml`. The example uses OVH but it can work with other providers, such as GoDaddy :<br>
  - Get the [required settings](https://go-acme.github.io/lego/dns/godaddy/) and update the `.env` file
  ```bash
    # DNS challenge credentials
    GODADDY_API_KEY=xxxxx
    GODADDY_API_SECRET=xxxxx
  ```
  - This is the only case where you are going to have to modify the docker-compose
  ```yaml
    environment:
      - GODADDY_API_KEY${GODADDY_API_KEY}
      - GODADDY_API_SECRET=${GODADDY_API_SECRET}
  ```

- **create the docker network** : As our services are split in multiple docker-compose, we need a network so that traefik can forward the requests. <br>
  ```bash
    sudo docker network create proxy
  ```

- **update the whitelist (optional)** : Replace the IP address in `rules/whitelist.yml`. Use the IP address as well as the [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing). Whitelist is disable by default with `0.0.0.0/0`. The whitelist will be used on containers setting the following label. <br>
  ```yaml
    # Ip filtering
    - "traefik.http.routers.service-router-name.middlewares=whitelist@file"
  ```
  You can use the private IP address range used by docker (172.16.0.0/12) if you are using [wireguard](../wireguard-pihole-unbound). Then your services will only be available through your VPN (recommend for a better security).

You can now run :

```bash
sudo docker-compose up -d
```
To check the logs :

```bash
sudo docker logs traefik
```

Traefik should be up and running ! To test if everything is running smoothly, you can try and use the [webserver](../webserver) service, it is a simple apache webserver showing `Hello World`. 
Keep in mind that traefik can take a little time to generate the first certificate, usually a couple of minutes.

## Note

If you want to use the [Redirect root to www](#redirect-root-to-www) fonctionnality, you also need to have a certificate generated for your root domain. In order to do so, you will need to use a service which uses the root domain.
The simplest way to do that is by running the [webserver](../webserver) service with the root domain. It only needs to be done once, you should then be able to see the entry in `letsencrypt/acme.json`, it will then be renewed automaticaly by traefik.

# Update

Both `traefik` and `socket-proxy` images are automatically updated with [watchtower](../watchtower) thanks to the following label :

```yaml
  # Watchtower Update
  - "com.centurylinklabs.watchtower.enable=true"
```