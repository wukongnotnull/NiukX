# NiukX

连接 1000 位牛人。让每个人拥有自己的社交网络。

这里是 **NiukX 的对外入口**：安装说明、版本清单、用户反馈。源码仓库是私有的，不用 clone 也能自托管。

需求、bug、安装问题请直接 [提 Issue](https://github.com/wukongnotnull/NiukX/issues/new)。

## 一键自托管

机器要求：Docker 20+，2 核 / 4GB / 20GB，放行 80 端口。

```bash
docker run -d \
  --name sns \
  -p 80:80 \
  -m 4g \
  -v sns-data:/data \
  -v /var/run/docker.sock:/var/run/docker.sock \
  --restart unless-stopped \
  wukongnotnull/sns:latest
```

首次启动约 1–2 分钟。查初始账号：

```bash
docker logs sns 2>&1 | grep -A6 "自托管初始账号"
# 或
docker exec sns cat /data/initial-admin.txt
```

会生成两个账号：`admin`（默认社区管理员）和 `super_admin`（跨租户超管）。

- 前台：`http://<公网IP>/`
- 后台：`http://<公网IP>/admin/`

更完整的环境变量、升级与备份说明见 [Docker Hub](https://hub.docker.com/r/wukongnotnull/sns)。

## 检查更新

已安装实例通过这份公开 JSON 检查是否有新版：

https://raw.githubusercontent.com/wukongnotnull/NiukX/main/latest.json

发新版时更新 `latest.json` 的 `version`、`releasedAt`、`notes`、`image`。
