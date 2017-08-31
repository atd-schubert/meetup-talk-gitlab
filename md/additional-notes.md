### Update GitLab

Just pull the images from docker-hub

```bash
docker-compose pull
docker-compose restart
```


### Stages

* `Package`: in master (and develop)
* `Test / Lint`: on merge in develop and master 
* `Deploy`: only for master


### Runner

* `shared`: Default
* `priority`: Just for projects that needs a higher priority
* `admin`: Only for admin purpose
* `{name}`: Specific runners for specific projects (higher priority)


### Artifacts

```yaml
package:
  stage: build
  script:
    - echo "Do something..."
  artifacts:
    name: "${CI_JOB_NAME}_${CI_COMMIT_REF_NAME}"
    paths:
      - "${CI_PROJECT_DIR}/dist/*"
    expire_in: 1 week

```


### GitLab-CE not on docker

* Run GitLab directly on your server (Port 22!)
* Run the runners in a docker swarm


### Provisioning script

Use this gist for a automated installation

https://gist.github.com/atd-schubert/aba495fa500472d04113a50dc78a6f07