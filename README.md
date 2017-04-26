# devtool(GitBucket/Jenkins/Redmine/Mattermost + Hubot)

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
