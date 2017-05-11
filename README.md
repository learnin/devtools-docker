# devtools(GitBucket/Jenkins/Redmine/Mattermost + Hubot)

## Getting started

```shell
export http_proxy=http://your_proxy_host:your_proxy_port/
export https_proxy=http://your_proxy_host:your_proxy_port/
export HTTP_PROXY=$http_proxy
export HTTPS_PROXY=$https_proxy
export no_proxy=`docker-machine ip default`
export NO_PROXY=$no_proxy

export MATTERMOST_HOST=Mattermost host # e.g. export MATTERMOST_HOST=192.168.99.100
export MATTERMOST_GROUP=Mattermost group # e.g. export MATTERMOST_GROUP=mmtest1
export MATTERMOST_USER=Mattermost bot user id # e.g. export MATTERMOST_USER=hubottest@example.jp
export MATTERMOST_PASSWORD=Mattermost bot user password # e.g. export MATTERMOST_PASSWORD=hubottest
export MATTERMOST_HTTP_PORT=Mattermost HTTP port # e.g. export MATTERMOST_HTTP_PORT=50002
export MATTERMOST_WSS_PORT=Mattermost WebSocket port # e.g. export MATTERMOST_WSS_PORT=50002
export MATTERMOST_TLS_VERIFY=true: verify TLS certs, false: not verify # e.g. export MATTERMOST_TLS_VERIFY=false
export MATTERMOST_USE_TLS=true: use https/wss to connect Mattermost, false: use http/ws # e.g. export MATTERMOST_USE_TLS=false
export HUBOT_JENKINS_URL=Jenkins URL # e.g. export HUBOT_JENKINS_URL=http://192.168.99.100:50001
export HUBOT_JENKINS_AUTH=jenkins_user_id:jenkins_user_password # e.g. export HUBOT_JENKINS_AUTH=admin:admin

docker-compose up -d
```

## How to backup
```shell
docker-compose stop
docker container run \
  --rm \
  -v devtoolsdocker_mattermost-db-data:/target/mattermost-db-data \
  -v devtoolsdocker_mattermost-app-config:/target/mattermost-app-config \
  -v devtoolsdocker_mattermost-app-data:/target/mattermost-app-data \
  -v devtoolsdocker_gitbucket-db-data:/target/gitbucket-db-data \
  -v devtoolsdocker_gitbucket-app-data:/target/gitbucket-app-data \
  -v devtoolsdocker_hubot-mattermost-data:/target/hubot-mattermost-data \
  -v devtoolsdocker_jenkins-data:/target/jenkins-data \
  -v devtoolsdocker_redmine-db-data:/target/redmine-db-data \
  -v devtoolsdocker_redmine-app-data:/target/redmine-app-data \
  -v $(pwd):/backup \
  ubuntu tar cvzfp /backup/backup.tar.gz /target
docker-compose start
```

If you use docker-machine, execute the above `docker container run` command in docker-machine, and copy backup.tar.gz from docker-machine to host machine with the following command.

```shell
docker-machine scp default:~/backup.tar.gz .
```

## How to restore
```shell
docker-compose stop
docker container run \
  --rm \
  -v devtoolsdocker_mattermost-db-data:/target/mattermost-db-data \
  -v devtoolsdocker_mattermost-app-config:/target/mattermost-app-config \
  -v devtoolsdocker_mattermost-app-data:/target/mattermost-app-data \
  -v devtoolsdocker_gitbucket-db-data:/target/gitbucket-db-data \
  -v devtoolsdocker_gitbucket-app-data:/target/gitbucket-app-data \
  -v devtoolsdocker_hubot-mattermost-data:/target/hubot-mattermost-data \
  -v devtoolsdocker_jenkins-data:/target/jenkins-data \
  -v devtoolsdocker_redmine-db-data:/target/redmine-db-data \
  -v devtoolsdocker_redmine-app-data:/target/redmine-app-data \
  -v $(pwd):/backup \
  ubuntu bash -c "cd /target && tar xvzfp /backup/backup.tar.gz --strip 1"
docker-compose start
```

If you use docker-machine, execute the following command to copy backup.tar.gz from host machine to docker-machine, and execute the above `docker container run` command in docker-machine.

```shell
docker-machine scp backup.tar.gz default:~/
```
