#### 启动一个简单的开发环境
* docker-compose安装
> https://docs.docker.com/compose/install/

* 启动mysql和redis
```bash
docker-compose -f ./docker-compose-db.yml up -d
```

* 启动最简单的Nacos环境

```bash
docker-compose -f ./nacos-docker/example/standalone-derby.yaml up -d
```

> `./docker-compose-db.yml` 为相对路径，前提是你要进入`docker`这个目录