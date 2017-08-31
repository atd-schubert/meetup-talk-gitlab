### Shared Runner

Runner to build projects from GitLab


### Add the runner in docker-compose

```yaml
version: '3'
services:
    gitlab:
        # ...
    admin-runner:
        # ...
    shared-runner:
        image: gitlab/gitlab-runner:latest
        volumes:
            - /var/run/docker.sock:/var/run/docker.sock
            - ./admin-runner/config:/etc/gitlab-runner
```


### Register the runner

```bash
docker-compose exec shared-runner gitlab-runner register
```


### Additional settings for the runner

```
[[runners]]
  [runners.docker]
    image = "acme/build"
    allowed_images = ["acme/*"]
    volumes = ["/cache" "/home/bob/.composer"]
    pull_policy = "if-not-present"
  [runners.cache]

```


### Example for an docker image to build php projects

```dockerfile
FROM php:latest

MAINTAINER Arne Schubert <atd.schubert@gmail.com>

RUN set -x \
  && apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
    git \
    zip unzip ca-certificates \
    openssh-client \
    curl \
    libsqlite3-dev \
  && rm -rf /var/lib/apt/lists/* \
  && curl -o /usr/bin/composer https://getcomposer.org/composer.phar \
  && chmod a+x /usr/bin/composer \
  && docker-php-source extract \
  && docker-php-ext-install pdo_sqlite \
  && docker-php-source delete \
  && useradd -ms /bin/bash bob

USER bob
```


### Build automated directly in GitLab

```yaml
stages:
  - build

package:
  stage: build
  tags:
    - admin
  only:
    - master
  script:
    - docker build -t acme/build:latest .
```

*Note: Use the admin-runner for that build*


### Create your dind image also from GitLab

You can create now the dind image the same way directly from GitLab!