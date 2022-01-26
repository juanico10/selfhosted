# About

#

<p align="center">
    <a href="https://js.wiki/">
        <img src="https://github.com/JuanRodenas/Docker-container-selfhosted/blob/main/wikijs/wikijs.png" alt="wikijs">
    </a>
    <br>
</p>
<!-- markdownlint-enable MD033 -->

#

Fail2ban scans log files and bans IPs that show the malicious signs.

* [Github](https://github.com/Requarks/wiki)
* [Documentation](https://docs.requarks.io/)
* [Docker Image](https://hub.docker.com/r/requarks/wiki)
* [Web](https://js.wiki/)

### Edit vars in docker-compose.yml
Edit the following variables, with the correct volume.
	- volumes: /patch/to/data/
	- Change the host variable with the domain you use for wikijs
	- Change the port to be used with wikijs
	- Change the network and enter the one you use for outdoor in traefik 

### Launch
	- `docker-compose -up d`

### View logs
	- `docker logs wikijs`

### Monitor traffic from a connected client,
	- Access to the container: `docker exec -it wikijs bash`

### Check
	- docker ps -a