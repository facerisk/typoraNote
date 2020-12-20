| docker命令                                        | 含义                         | 备注 |
| :------------------------------------------------ | :--------------------------- | :--: |
| docker -v                                         | 查看docker版本               |      |
| docker search redis                               | 检索redis                    |      |
| docker pull redis                                 | 下载redis镜像                |      |
| docker images                                     | 查看镜像列表                 |      |
| docker rmi image-id                               | 根据镜像id删除               |      |
| docker rmi $(docker images -q)                    | 删除所有镜像                 |      |
| docker run --name container-name -d image-name    | 容器启动                     |      |
| docker ps                                         | 查看运行中容器列表           |      |
| docker ps -a                                      | 查看运行/停止中容器列表      |      |
| docker stop container-name/container-id           | 停止容器                     |      |
| docker start container-name/container-id          | 启动容器                     |      |
| docker run -d -p 6378:6379 --name port-reds redis | 映射端口到本机 redis默认6379 |      |
| docker rm container-id                            | 删除单个容器                 |      |
| docker rm $(docker ps -a -q)                      | 删除所有容器                 |      |
| docker logs container-name/container-id           | 查看当前容器日志             |      |
| docker exec -it container-name/container-id bash  | 登录容器                     |      |
|                                                   |                              |      |
|                                                   |                              |      |
|                                                   |                              |      |

