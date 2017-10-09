docker-sample
====

This is docker sample

## Build with compose
```
$ docker-compose up -d --build
```

## Get into container
```
$ docker exec -it docker_workspace_1 bash
```

## Stop running
```
$ docker-compose stop
```

## IP(Docker for Mac)
```
127.0.0.1
```

## ADD HOST
```
$ sudo sh -c "echo 127.0.0.1 docker.local >> /etc/hosts"
```

## ADD SSH CONFIG(Modify $PATH by yourself)
```
printf "\
Host docker.local
  HostName 127.0.0.1
  User devadmin
  Port 10080
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  LogLevel FATAL
  IdentityFile ~/$PATH/docker/workspace/id_rsa
" | cat >> ~/.ssh/config
```

## Get into container with ssh
```
$ ssh docker.local
```

## Referense
* [docker-compose](https://docs.docker.com/compose/compose-file/)
* [docker-compose-build](https://docs.docker.com/compose/reference/build/)
* [Install Docker for Mac](https://docs.docker.com/docker-for-mac/install/)
