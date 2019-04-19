## awanderfulvirtualscan(awvs)

版本来源为：https://www.52pojie.cn/thread-922535-1-1.html

**仅供学习**

本来想写一个可以自己构建的版本，但是发现在使用patch的时候出了些问题，没有搞定。所以只好自己手动提交了一个镜像，镜像有点大。

由于没有挂载数据，所以如果想保存结果就别删容器。

### 全自动的版本

docker-compose.yml

```yaml
version: "3"

services:
  awanderfulvirtualscan:
    image: registry.cn-hangzhou.aliyuncs.com/o1hy/tools:awanderfulvirtualscan
    ports:
      - "3443:13443"
```

`docker-compose up`

登录账号为：`last@last.com` 密码：`123!@#qwe`

### 半自动

先自行去https://www.52pojie.cn/thread-922535-1-1.html下载内容。解压后放在半自动文件夹内。

```dockerfile
FROM ubuntu:16.04
COPY ./sources.list /etc/apt/sources.list
COPY ./acunetix_trial.sh /acunetix_trial.sh
COPY ./patch_awvs /patch_awvs
RUN chmod +x /acunetix_trial.sh/acunetix_trial.sh &&  apt-get update && apt-get install -y libxdamage1 libgtk-3-0 libasound2 libnss3 libxss1 sudo bzip2 
RUN mv /patch_awvs/patch_awvs /home/acunetix/.acunetix_trial/v_190325161/scanner/
USER acunetix
RUN /home/acunetix/.acunetix_trial/v_190325161/database/bin/pg_ctl -D /home/acunetix/.acunetix_trial/db -l logfile start
USER root
```

需要自行进入容器后，先通过**acunetix** 用户执行执行 `/bin/bash /home/acunetix/.acunetix_trial/start.sh` 然后通过root用户`/home/acunetix/.acunetix_trial/v_190325161/scanner/patch_awvs` 

账号密码同上。

### 全手动

打扰了。