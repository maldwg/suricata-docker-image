# suricata-docker-image
![Docker Image Version](https://img.shields.io/docker/v/maxldwg/suricata?label=Latest%20version%20build)

Project to package suricata into a ubuntu based docker image.
The installation is conducted as stated by the official documentation.

## Usage

The image starts a container using no special command. In order to use the suricata functionalities properly, start a container with the respective suricata command, as documented in the official [suricata documentation](https://docs.suricata.io/en/latest/). 


It is recommended to use the container in host network mode to allow it to run in promiscuous mode. 

```
docker run -it --name suricata \
                --network host \
                --cap-add NET_ADMIN \
                maxldwg/suricata "suricata --help"
```