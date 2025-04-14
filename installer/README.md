# 构建镜像并推送到远程仓库

1. 进入工作目录
```shell
cd knowledge-base
```
2. 构建本地镜像
```shell
docker build -f .\installer\Dockerfile --progress=plain -t adq-maxkb:v1.10.4-lts .
```
3. 添加镜像标签
```shell
docker tag adq-maxkb:v1.10.4-lts [ip]/[path]/adq-maxkb:v1.10.4-lts 
```
4. 推送镜像到远程仓库
```shell
docker push [ip]/[path]/adq-maxkb:v1.10.4-lts
```
5. 相关问题
```text
1. 构建镜像时 run-maxkb.sh 或 start-maxkb.sh 脚本执行失败，脚本文件的换行符换成unix的"LF"。
2. 构建镜像时 npm run build 执行失败，将 package.json 文件中的 "set NODE_OPTIONS=--max_old_space_size=4096" 改成 "export NODE_OPTIONS=--max_old_space_size=4096"。
```

# 创建并启动容器

1. 创建 docker-compose.yml 文件
```yml
services:
  adq-maxkb:
    image: [ip]/[path]/adq-maxkb:v1.10.4-lts
    container_name: adq-maxkb
    restart: unless-stopped
    ports:
      - 28080:8080
    networks:
      - adq-max-network
    volumes:
      - ./data:/var/lib/postgresql/data
      - ./python-packages:/opt/maxkb/app/sandbox/python-packages
    labels:
      createdBy: "ADQ"
networks:
  adq-max-network:
    driver: bridge
```
2. 启动容器
```shell
docker compose up -d
```
