# Docker 部署指南

## 飞牛NAS / 任意 Docker 环境部署

### 快速开始

```bash
# 1. 进入 docker 目录
cd docker

# 2. 复制配置文件，填入账号密码
cp .env.example .env
nano .env

# 3. 启动
docker-compose up -d

# 4. 查看日志
docker-compose logs -f
```

### 配置说明

编辑 `.env` 文件：

| 变量 | 必填 | 默认值 | 说明 |
|------|------|--------|------|
| `LINUXDO_USERNAME` | ✅ | - | Linux.do 用户名 |
| `LINUXDO_PASSWORD` | ✅ | - | Linux.do 密码 |
| `RUNS_PER_DAY` | ❌ | 2 | 每天运行次数 |
| `TOPICS_MIN` | ❌ | 15 | 每次最少浏览帖子数 |
| `TOPICS_MAX` | ❌ | 40 | 每次最多浏览帖子数 |
| `LIKE_RATE` | ❌ | 30 | 点赞概率 (0-100) |
| `RUN_ON_START` | ❌ | true | 启动时是否立即运行一次 |

### 运行机制

- 启动后立即执行一次浏览任务
- 之后每天在 7:00-23:00 之间随机选择时间运行
- 每次运行时间、浏览数量、点赞都是随机的
- 浏览器数据持久化，登录状态会保持

### 常用命令

```bash
# 启动
docker-compose up -d

# 停止
docker-compose down

# 查看日志
docker-compose logs -f

# 重启
docker-compose restart

# 重新构建（更新代码后）
docker-compose up -d --build

# 只运行一次（不启动调度器）
docker-compose run --rm linuxdo --once
```

### 资源占用

- 内存限制: 1GB
- CPU 限制: 1 核
- 磁盘: Chrome 数据约 200MB
