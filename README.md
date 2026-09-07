# NiukX

连接 1000 位牛人。让每个人拥有自己的社交网络。

这里是 **NiukX 的对外入口**：安装说明、版本清单、用户反馈。

需求、bug、安装问题请直接 [提 Issue](https://github.com/wukongnotnull/NiukX/issues/new)。

## 能做什么

- **私域社区**：专属会员空间，沉淀高价值用户，建立品牌私域流量池
- **知识付费**：课程、专栏、直播打赏，多种形式实现知识变现
- **粉丝圈**：KOL、创作者与粉丝深度互动，打造专属粉丝阵地
- **垂直社区**：行业、兴趣、地域等多维度聚合，精准连接同路人
- **轻电商**：社区内嵌商品、订单、支付，内容与交易无缝打通
- **即时社交**：实时消息、群聊、@提醒，提升社区活跃与粘性

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
