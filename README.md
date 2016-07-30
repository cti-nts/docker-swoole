docker-swoole
=============

Collection of different swoole-docker solution for you reference.

## betashepherd/

**Get Docker Swoole Image**
```shell
docker pull betashepherd/docker-swoole
docker images
```

**Run docker-swoole image**
```shell
docker run -i -t betashepherd/docker-swoole:1.7.15-stable /bin/bash
bash-4.1# su swoole 
bash-4.1$ cd ~
bash-4.1$ pwd
/home/swoole
bash-4.1$ php -r "echo SWOOLE_VERSION;"
```


## [deprecated] [alpine_php7_runtime_with_swoole/](./auto_alpine_php7_runtime_with_swoole/)

php7-runtime +swoole based on alpine-edge.  Build from PECL, and some patches needed to finish compile.
As building from source directly is tested (see below), so this folder is deprected while kept only for reference.

## [alpine_php7_runtime_with_swoole/](./auto_alpine_php7_runtime_with_swoole_latest/)

php7(latest)-runtime +swoole based on alpine-edge, which build from [swoole-src](https://github.com/swoole/swoole-src/) directly.

## LINKS

*Install Docker*
[Visit Docker-Doc](https://docs.docker.com/)

