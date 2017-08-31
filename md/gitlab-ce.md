### GitLab Community edition

GitLab is a web-based Git repository manager with wiki and issue tracking features, using an open source license


### Prepare GitLab in docker-compose

```yaml
version: '3'
services:
    gitlab:
        image: gitlab/gitlab-ce:latest
        volumes:
            - /var/run/docker.sock:/var/run/docker.sock
            - ./gitlab-ce:/etc/gitlab
            - gitlab-data:/var/opt/gitlab
            - gitlab-logs:/var/log/gitlab
        environment:
            GITLAB_OMNIBUS_CONFIG: "external_url 'http://gitlab.acme.com/'; gitlab_rails['lfs_enabled'] = true;"
        ports:
            - 80:80
            - 443:443
            - 44:22
volumes:
    gitlab-data:
    gitlab-logs:
```


### SSH Port

**Be careful with the SSH port 22!**


### Update permissions

If you run into access problems:

```bash
docker-compose exec gitlab update-permissions
```


### Install GitLab without docker

[about.gitlab.com/installation](https://about.gitlab.com/installation/)

```bash
apt-get install -y curl openssh-server ca-certificates
curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash
apt-get install gitlab-ce
gitlab-ctl reconfigure
```


### Set a root user

Go to your GitLab server with a browser of choice and register the root user
