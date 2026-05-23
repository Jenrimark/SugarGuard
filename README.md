<div align="center">

# 糖知 SugarGuard

**青少年智能控糖助手**

基于 Android + Spring Boot + AI 的血糖健康管理平台，帮助青少年科学监控每日糖分摄入

[![Android](https://img.shields.io/badge/Android-7.0%2B-green?logo=android)]()
[![Kotlin](https://img.shields.io/badge/Kotlin-1.9.20-purple?logo=kotlin)]()
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-2.7.18-brightgreen?logo=springboot)]()
[![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python)]()
[![License](https://img.shields.io/badge/License-Private-red)]()

</div>

---

## 项目简介

糖知是一款面向青少年的智能控糖应用，通过 **AI 图像识别**、**RAG 知识库** 和 **DeepSeek 大模型**，帮助用户轻松记录饮食、分析糖分摄入、获取个性化健康建议。

### 核心功能

| 功能 | 说明 |
|------|------|
| 首页仪表盘 | 每日糖分摄入环形进度、健康评分（0-100）、各餐次糖分明细 |
| 饮食日记 | 日历视图查看历史记录，周度糖分趋势图表 |
| 拍照识别 | 基于 Google ViT 模型的本地/远程食物图像识别，自动获取营养信息 |
| AI 助手 | DeepSeek 大模型驱动的多轮健康问答，集成 RAG 知识库 |
| 智能推荐 | 基于用户偏好 + 健康档案 + 协同过滤的饮品推荐 |
| 健康分析 | 多维健康数据图表、BMI 分析、糖分摄入评估 |
| 成就系统 | 控糖打卡徽章，激励持续健康习惯 |
| 消息通知 | 定时提醒、健康建议推送 |

---

## 技术架构

```
┌─────────────────────────────────────────────────┐
│              Android App (Kotlin)               │
│   Jetpack Compose · Room · Retrofit · ML Kit    │
└──────────────────────┬──────────────────────────┘
                       │ HTTP/REST
┌──────────────────────▼──────────────────────────┐
│           Backend API (Spring Boot)             │
│   Spring Security · JWT · JPA · MySQL           │
└──────────────────────┬──────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────┐
│           AI Service (Python/FastAPI)           │
│   DeepSeek · ViT · FAISS · RAG · LangChain     │
└─────────────────────────────────────────────────┘
```

### 技术栈

**移动端**
- Kotlin + Jetpack Compose (Material 3)
- Room 本地数据库 · Retrofit + OkHttp 网络层
- Google ML Kit 端侧图像识别 · Coil 图片加载

**后端服务**
- Spring Boot 2.7 + Spring Security + JWT 认证
- Spring Data JPA + MySQL 8.0

**AI 服务**
- FastAPI + DeepSeek 大模型（LangChain 集成）
- Google ViT 图像分类 · FAISS 向量检索
- sentence-transformers 多语言嵌入 · RAG 知识库

**基础设施**
- Docker Compose 编排（10 个服务）
- Nginx 反向代理 · Redis 缓存
- Prometheus + Grafana 监控
- ELK 日志采集（Elasticsearch + Logstash + Kibana）

---

## 项目结构

```
SugarGuard/
├── app/                    # Android 客户端
│   └── src/main/java/com/example/myapplication/
│       ├── ui/compose/     # 31 个 Compose 页面
│       ├── api/            # Retrofit API 接口
│       ├── model/          # 数据模型
│       ├── viewmodel/      # ViewModel 层
│       ├── db/             # Room 数据库（Entity, DAO）
│       └── util/           # 工具类
├── backend-api/            # Spring Boot 后端
│   └── src/main/java/com/example/usermanagement/
│       ├── controller/     # 17 个 REST 控制器
│       ├── service/        # 业务逻辑
│       ├── entity/         # JPA 实体
│       └── dto/            # 数据传输对象
├── ai-service/             # Python AI 服务
│   ├── main.py             # FastAPI 入口
│   ├── agents/             # AI 智能体（对话、推荐、RAG）
│   ├── tools/              # 工具（图像识别、健康评估）
│   └── scrapers/           # 数据爬虫
├── scripts/                # 部署与数据脚本
├── doc/                    # Sprint 项目文档
├── docker-compose.yml      # Docker 编排配置
└── gradle/                 # Gradle 版本目录
```

---

## 快速开始

### 环境要求

| 组件 | 版本要求 |
|------|----------|
| Android Studio | Hedgehog+ |
| JDK | 11+ |
| Python | 3.10+ |
| MySQL | 8.0+ |
| Docker | 20.10+（可选） |

### Android 客户端

```bash
# 使用 Android Studio 打开项目根目录
# 或命令行构建
./gradlew assembleDebug
```

### 后端服务

```bash
cd backend-api
mvn package
java -jar target/user-management-*.jar
```

### AI 服务

```bash
cd ai-service
pip install -r requirements.txt
cp config.example.env .env
# 编辑 .env 配置 DeepSeek API Key 和数据库连接
python main.py
```

服务启动后访问 `http://localhost:8000/docs` 查看 API 文档。

### Docker 一键部署

```bash
# 开发环境
docker-compose up -d

# 生产环境
bash scripts/deploy.sh production
```

---

## 文档

项目文档位于 `doc/` 目录：

| 阶段 | 内容 |
|------|------|
| Sprint 0 | 原型设计、用户画像、架构设计、竞品分析、项目计划 |
| Sprint 1 | 环境初始化、Docker 编排、AI 部署、单元/API 测试、SonarQube |
| Sprint 2 | RAG 知识库、FAISS 向量库、ViT 调优、AI 对话、智能推荐 |
| Sprint 3 | JMeter 压测、全量验收、v1.0.0 正式发布 |
| 代码规范 | 编码规范、Git 分支策略 |

---

## 许可证

本项目为私有仓库，未经授权禁止使用和分发。
