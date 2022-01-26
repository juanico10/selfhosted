# About

#

<p align="center">
    <a href="https://heimdall.site/">
        <img src="https://github.com/JuanRodenas/Docker-container-selfhosted/tree/main/Heimdall/heimdall.png" alt="heimdall">
    </a>
    <br>
</p>
<!-- markdownlint-enable MD033 -->

#

Fail2ban scans log files and bans IPs that show the malicious signs.

* [Github](https://github.com/linuxserver/Heimdall)
* [Documentation](https://heimdall.site/)
* [Docker Image](https://hub.docker.com/r/linuxserver/heimdall/)

### Edit vars in docker-compose.yml
Edit the following variables, with the correct volume.
	- volumes: /patch/to/data/
	- Change the host variable with the domain you use for heimdall
	- Change the port to be used with heimdall
	- Change the network and enter the one you use for outdoor in traefik

### Launch
	- `docker-compose -up d`

### View logs
	- `docker logs heimdall`

### Monitor traffic from a connected client,
	- Access to the container: `docker exec -it heimdall bash`

### Check
	- docker ps -a