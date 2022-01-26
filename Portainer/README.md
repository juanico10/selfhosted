# About

#

<p align="center">
    <a href="https://www.portainer.io/">
        <img src="https://github.com/JuanRodenas/Docker-container-selfhosted/blob/main/Portainer/portainer.png" alt="portainer">
    </a>
    <br>
</p>
<!-- markdownlint-enable MD033 -->

#

Fail2ban scans log files and bans IPs that show the malicious signs.

* [Github](https://github.com/portainer/portainer)
* [Documentation](https://docs.portainer.io/)
* [Docker Image](https://hub.docker.com/r/portainer/portainer)

### Edit vars in docker-compose.yml
Edit the following variables, with the correct volume.
	- volumes: /patch/to/data/
	- Change the host variable with the domain you use for portainer
	- Change the port to be used with portainer
	- Change the network and enter the one you use for outdoor in traefik 

### Launch
	- `docker-compose -up d`

### View logs
	- `docker logs portainer`

### Monitor traffic from a connected client,
	- Access to the container: `docker exec -it portainer bash`

### Check
	- docker ps -a