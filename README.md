### Rust环境
```bash
docker build rust-os:v0.1 .
docker run -d --privileged -v /d:/daily:/usr/daily -p 58888:8080 rust-os:v0.1
# --privileged (赋予等同主机的特权)
# 58888:8080 HOST_PORT:CONTAINER_PORT
# HOST_PORT：主机上要接收流量的端口号
# CONTAINER_PORT：容器内侦听连接的端口号
# 本地访问 [local]http://localhost:58888/ 进行开发 
```
### 工作环境
```bash
docker build work-server:v0.1 .
docker run -d --privileged -v /d:/Code:/usr/Code -v /d:/daily:/usr/daily -p 56888:8080 work-server:v0.1
```