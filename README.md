# NiukX

连接 1000 位牛人。

让每个人都拥有自己的社交网络。

这里是 **NiukX 的对外入口**：安装说明、版本清单、用户反馈。

安装或使用中遇到问题，请直接 [提 Issue](https://github.com/wukongnotnull/NiukX/issues/new)。

## 能做什么

- **私域社区**：专属会员空间，沉淀高价值用户，建立品牌私域流量池
- **知识付费**：课程、专栏、直播打赏，多种形式实现知识变现
- **粉丝圈**：KOL、创作者与粉丝深度互动，打造专属粉丝阵地
- **垂直社区**：行业、兴趣、地域等多维度聚合，精准连接同路人
- **轻电商**：社区内嵌商品、订单、支付，内容与交易无缝打通
- **即时社交**：实时消息、群聊、@提醒，提升社区活跃与粘性

## 一键自托管

你需要：已安装 Docker 20 或更高版本的服务器，建议 2 核 / 2GB / 20GB，放行 80 端口。

**海外**（Docker Hub）：

```bash
docker run -d \
  --name sns \
  -p 80:80 \
  -m 2g \
  -v sns-data:/data \
  -v /var/run/docker.sock:/var/run/docker.sock \
  --restart unless-stopped \
  wukongnotnull/sns:latest
```

**国内**（阿里云镜像，通常更快）：

```bash
docker run -d \
  --name sns \
  -p 80:80 \
  -m 2g \
  -v sns-data:/data \
  -v /var/run/docker.sock:/var/run/docker.sock \
  --restart unless-stopped \
  crpi-6hpz6udbnjhvzeit.cn-shanghai.personal.cr.aliyuncs.com/wukongnotnull/sns:latest
```

命令里那行 `docker.sock`：加上去，以后就能在后台点一下升级；去掉也能用，按 [Docker Hub](https://hub.docker.com/r/wukongnotnull/sns) 上的「手动升级」自己更新。加上后，容器能控制这台机器的 Docker，请只装在自己的服务器上。

第一次启动大约 1–2 分钟。查看初始用户名和密码：

```bash
docker logs sns 2>&1 | grep -A6 "自托管初始账号"
# 或
docker exec sns cat /data/initial-admin.txt
```

第一次安装会创建两个管理员，登录后请尽快修改密码：

| 角色 | 用户名 | 默认密码 | 能做什么 |
| --- | --- | --- | --- |
| 跨租户超级管理员 | `superadmin` | `@superadmin123` | 管理全部社区，并可升级系统 |
| 默认社区租户管理员 | `admin` | `@admin123` | 只管理自动生成的默认社区 |

把 `<公网IP>` 换成你的服务器 IP。两种管理员请走各自的后台，不要混用。

- 前台（给社区成员用）：`http://<公网IP>/`
- 跨租户超级管理员后台：`http://<公网IP>/admin/superadmin/`
- 社区租户管理员后台：`http://<公网IP>/admin/<租户代码>/`

第一次安装自动新建默认社区 `default`，社区管理员请打开 `http://<公网IP>/admin/default/`。以后新建的社区，把地址里的 `default` 换成那个社区的代码即可。

升级、备份等完整说明见 [Docker Hub](https://hub.docker.com/r/wukongnotnull/sns)。

## 检查更新

已安装的系统通过这份公开清单检查是否有新版：

https://raw.githubusercontent.com/wukongnotnull/NiukX/main/latest.json
