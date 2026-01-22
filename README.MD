# DriftingWind forked (自用)
## 修改内容：
 1. 手动 Actions，推送到 ghcr.io
 2. 参考 xray 原项目，调整了一下编译环境。只编译 amd64 版本，加快编译速度
 3. 适当缩短镜像 tag 和链接地址，也为了和 wulabing 大佬原版做区分
 4. 添加 docker-compose.yml 参考内容等，也可以点下方传送门查看 wulabing 大佬的持久化配置

[![xray_docker_reality_docker_image_build](https://github.com/DriftingWind/xray_docker/actions/workflows/xray_docker_reality.yml/badge.svg)](https://github.com/DriftingWind/xray_docker/actions/workflows/xray_docker_reality.yml)
[![xray_docker_xhttp_reality_docker_image_build](https://github.com/DriftingWind/xray_docker/actions/workflows/xray_docker_xhttp_reality.yml/badge.svg)](https://github.com/DriftingWind/xray_docker/actions/workflows/xray_docker_xhttp_reality.yml)

## reality 参考 docker-compose.yml
```YAML
services:
  reality:
    image: ghcr.io/driftingwind/xray_docker_reality:latest
    container_name: reality
    restart: always
    ports:
      - "20443:443" # 宿主机端口和下面的 EXTERNAL_PORT 要同步修改
    environment:
      EXTERNAL_PORT: "20443"
      DEST: ""
      SERVERNAMES: ""
      # 下面三个变量可以在运行一次容器后，将随机生成的值填入来固化
      UUID: ""
      PRIVATEKEY: ""
      PUBLICKEY: ""
    logging:
      options:
        max-size: "100m"
        max-file: "3"
```

## xhttp 参考 docker-compose.yml
```YAML
services:
  xhttp:
    image: ghcr.io/driftingwind/xray_docker_xhttp_reality:latest
    restart: always
    container_name: xhttp
    ports:
      - '30443:443' # 宿主机端口和下面的 EXTERNAL_PORT 要同步修改
    environment:
      EXTERNAL_PORT: "30443"
      DEST: ""
      SERVERNAMES: ""
      # 下面四个变量可以在运行一次容器后，将随机生成的值填入来固化
      UUID: ""
      PRIVATEKEY: ""
      PUBLICKEY: ""
      XHTTP_PATH: ""
    logging:
      options:
        max-size: "100m"
        max-file: "3"
```
## 升级脚本 update.sh
```BASH
#!/bin/bash
set -e

docker compose pull
docker compose down
docker compose up -d
```

以下是原 README.MD 内容
* * *
## xray_docker_reality
xray reality docker 镜像

[![xray_docker_reality_docker_image_build](https://github.com/wulabing/xray_docker/actions/workflows/xray_docker_reality.yml/badge.svg)](https://github.com/wulabing/xray_docker/actions/workflows/xray_docker_reality.yml)
![xray_docker_xhttp_reality_docker_image_build](https://github.com/wulabing/xray_docker/actions/workflows/xray_docker_xhttp_reality.yml/badge.svg)

## 注意事项
请确保在使用前已正确安装和配置 XRay 客户端。
为了保证安全和稳定，请勿将 UUID、私钥等敏感信息泄露给他人。

## 如何寻找合适的 SERVERNAMES 及 DEST

可以直接使用 docker 容器提供的默认值
您也可以自行寻找合适的 SERVERNAMES 及 DEST，请参考 [Reality - TLS - Scanner](https://github.com/XTLS/RealiTLScanner)

## 传送门

- [xray_docker_reality](https://github.com/wulabing/xray_docker/tree/master/reality)
- [xray_docker_xhttp_reality](https://github.com/wulabing/xray_docker/tree/master/xhttp_reality)

## 捐赠

您可以使用我的 搬瓦工 AFF 购买 VPS

https://bandwagonhost.com/aff.php?aff=63939

您可以使用我的 JustMySocks AFF 购买搬瓦工提供的代理

https://justmysocks.net/members/aff.php?aff=17621

您可以使用我的 DMIT AFF 购买 VPS

https://www.dmit.io/aff.php?aff=3957

您可以使用我的 Vultr AFF 创建新的 Vultr 账号并使用

https://www.vultr.com/?ref=6881279

您可以使用我的 nube AFF 购买按量付费VPS

https://nube.sh/invite/5986088028ENM0

您可以通过 USDT 支持我，感谢您的支持
TRC20: TU8mLTPfa5Y9nmszyfyt2VRAtuZhdLexL8
