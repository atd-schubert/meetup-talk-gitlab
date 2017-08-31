### Pre-Requirements

* [Docker](https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/)
* [docker-compose](https://docs.docker.com/compose/install/)


### Pre-Requirements Ubuntu

```bash
apt-get update \
  && apt-get install -y \
    linux-image-extra-virtual \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common \
  && echo "Register docker software-repository..." \
  && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - \
  && add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) \
    stable" \
  && echo "Install docker..." \
  && apt-get update \
  && apt-get install -y docker-ce \
  && echo "Install docker-compose..." \
  && curl -L https://github.com/docker/compose/releases/download/$DOCKER_COMPOSE_VERSION/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose \
  && chmod +x /usr/local/bin/docker-compose
```
