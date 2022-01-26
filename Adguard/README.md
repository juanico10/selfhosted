# About
Docker container Adguard

#

<p align="center">
    <a href="https://adguard.com/es/adguard-home/overview.html">
        <img src="https://github.com/JuanRodenas/Docker-container-selfhosted/blob/main/Adguard/adguard.png" alt="fail2ban">
    </a>
    <br>
</p>
<!-- markdownlint-enable MD033 -->

#
* [Github](https://github.com/AdguardTeam/AdGuardHome)
* [Documentation](https://kb.adguard.com/en/home/overview)
* [Docker Image](https://hub.docker.com/_/nextcloud)
* [Web](https://adguard.com/es/adguard-home/overview.html)

### Edit vars in docker-compose.yml
Edit the following variables, with the correct volume.
	- volumes: /patch/to/data/
	- Open ports on the router, and point it to the IP of the server where you are running the container. 

### Launch
	- `docker-compose -up d`

### View logs
	- `docker logs adguard`

### Monitor traffic from a connected client,
	- Access to the container: `docker exec -it adguard bash`

### Check
	- docker ps -a