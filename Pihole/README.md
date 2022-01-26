## Docker Pi-Hole for RaspberryPi :strawberry: / NanoPi NEO :snake:

<p align="center">
        <img src="icon.png" alt="PNG" height="300px" />
</p>

### Requeriments
- Raspberry Pi / NanoPi NEO2 or NEO3
- Raspbian OS / DietPi
- Service docker running

### Install Docker
    sudo apt update
    sudo apt upgrade -y
    sudo apt install -y libffi-dev libssl-dev python3 python3-pip
    sudo curl -sSL https://get.docker.com | sh
    sudo usermod -aG docker $USER
    sudo apt install -y docker-compose

### Edit vars in docker-compose.yml
Edit the following variables, with the correct interface and IP of the RasPi.

    INTERFACE: eth0
    WEBPASSWORD: YOUR_PASSWD


### Running
    docker-compose up -d

### Check
    docker ps -a