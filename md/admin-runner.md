### Admin Runner

Runner with a connection to the docker ecosystem

Creates docker images for other CI runners


### Add the runner in docker-compose

```yaml
version: '3'
services:
    gitlab:
        # ...
        expose:
            - 80
            - 443
            - 22
    admin-runner:
        image: gitlab/gitlab-runner:latest
        volumes:
            - /var/run/docker.sock:/var/run/docker.sock
            - ./admin-runner/config:/etc/gitlab-runner
```


### Register the runner

```bash
docker-compose exec admin-runner gitlab-runner register
```

*Recommendation: Register this runner as a specific runner to a secured repository*


### Additional settings for the runner

```
[[runners]]
  [runners.docker]
    image = "acme-dind"
    allowed_images = ["acme*"]
    volumes = ["/cache", "/var/run/docker.sock:/var/run/docker.sock"]
    pull_policy = "if-not-present"
  [runners.cache]

```


### Dockerfile for "dind" in admin runner

```dockerfile
FROM alpine:latest

MAINTAINER Arne Schubert <atd.schubert@gmail.com>

RUN set -x \
  && apk --no-cache add docker

VOLUME ["/var/run/docker.sock"]
```


### Build it up!

```bash
docker build -t acme-dind .
```


### What means dind?

**Docker in Docker**

* Independent
* Dependent

