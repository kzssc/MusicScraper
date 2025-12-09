# MusicScraper

<p align="center">
  <img src="docs/images/logo.png" alt="Music Scraper Logo" width="120">
</p>

<h1 align="center">🎵 Music Scraper</h1>

<p align="center">
  <strong>专为 NAS 用户打造的音乐元数据刮削工具</strong>
</p>

<p align="center">
  <a href="#-功能特性">功能特性</a> •
  <a href="#-界面预览">界面预览</a> •
  <a href="#-快速部署">快速部署</a> •
  <a href="#-使用指南">使用指南</a> •
  <a href="#-常见问题">常见问题</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Docker-Ready-2496ED?style=flat-square&logo=docker&logoColor=white" alt="Docker">
  <img src="https://img.shields.io/badge/Python-3.9+-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/License-MIT-green?style=flat-square" alt="License">
  <img src="https://img.shields.io/badge/Platform-NAS-orange?style=flat-square" alt="Platform">
</p>

---

## 📖 项目简介

**Music Scraper** 是一款轻量级的音乐元数据刮削工具，帮助你自动获取音乐文件的封面、歌词、艺术家等信息。专为 NAS（网络存储）用户设计，支持 Docker 一键部署，通过网页即可在手机/电脑上操作。

### 🎯 解决什么问题？

- 音乐文件没有封面，播放器显示空白？
- 歌曲信息不完整，无法按专辑/艺术家分类？
- 手动一首首填写信息太麻烦？

**Music Scraper 帮你自动完成这些工作！**

---

## ✨ 功能特性

| 功能 | 说明 |
|------|------|
| 🎯 **多数据源** | 支持企鹅、云村、酷系、苹果、开放库等 6 大音乐数据源 |
| 🖼️ **智能匹配** | 基于置信度算法自动选择最佳匹配结果 |
| 📱 **移动端适配** | 赛博朋克风格 UI，支持手机/平板访问 |
| 🚀 **一键部署** | Docker 镜像开箱即用，专为 NAS 优化 |
| 📦 **批量处理** | 支持整个文件夹自动批量刮削 |
| 🎵 **多格式支持** | MP3、FLAC、M4A、OGG、WAV、WMA 等 |
| 📝 **歌词获取** | 自动下载歌词并保存为 LRC 文件 |
| 🔄 **多源互补** | 首选源缺少数据时，自动从其他源补充 |

---

## 🎨 界面预览

### 首页

赛博朋克风格设计，深邃暗色背景配合霓虹色彩。

<!-- 📸 截图位置：首页截图，展示整体界面风格 -->
<!-- 建议截图：打开首页，展示功能入口卡片和音乐库统计卡片 -->
![首页预览](docs/images/screenshot-home.png)

### 文件浏览

支持目录导航，快速定位音乐文件。

<!-- 📸 截图位置：文件浏览页截图 -->
<!-- 建议截图：打开文件浏览页，展示目录列表和音乐文件 -->
![文件浏览](docs/images/screenshot-browser.png)

### 手动刮削

选择数据源，搜索并匹配歌曲信息。

<!-- 📸 截图位置：手动刮削页截图 -->
<!-- 建议截图：打开一首歌的刮削页面，展示搜索结果列表 -->
![手动刮削](docs/images/screenshot-scrape.png)

### 自动刮削

一键批量处理，智能匹配最佳结果。

<!-- 📸 截图位置：自动刮削页截图 -->
<!-- 建议截图：展示自动刮削的配置界面或刮削进度 -->
![自动刮削](docs/images/screenshot-auto-scrape.png)

### 音乐库统计

可视化展示音乐库元数据完整度。

<!-- 📸 截图位置：统计页截图 -->
<!-- 建议截图：展示统计页面的各项数据和进度条 -->
![音乐库统计](docs/images/screenshot-stats.png)

---

## 🚀 快速部署

### 方式一：Docker 命令行（推荐）

```bash
# 运行容器
docker run -d \
  --name music-scraper \
  -p 7301:7301 \
  -v /你的音乐目录:/app/music \
  -v music-scraper-data:/app/data \
  -e TZ=Asia/Shanghai \
  --restart unless-stopped \
  your-dockerhub-username/music-scraper:latest
```

访问 `http://你的IP:7301` 即可使用。

### 方式二：Docker Compose

创建 `docker-compose.yml` 文件：

```yaml
version: '3'
services:
  music-scraper:
    image: your-dockerhub-username/music-scraper:latest
    container_name: music-scraper
    ports:
      - "7301:7301"
    volumes:
      - /你的音乐目录:/app/music       # 修改为你的音乐文件夹路径
      - music-scraper-data:/app/data   # 数据持久化
    environment:
      - TZ=Asia/Shanghai
    restart: unless-stopped

volumes:
  music-scraper-data:
```

运行：

```bash
docker-compose up -d
```

### 方式三：NAS 手动导入镜像

适用于无法直接拉取镜像的 NAS 设备（如绿联云 NAS）。

1. **下载镜像文件**

   从 [Releases](https://github.com/your-username/music-scraper/releases) 页面下载：
   - `music-scraper-amd64.tar`（x86 架构，适用于绿联、威联通等）
   - `music-scraper-arm64.tar`（ARM 架构，适用于部分群晖）

2. **上传到 NAS**

   将 `.tar` 文件上传到 NAS 的任意目录。

3. **导入镜像**

   <!-- 📸 截图位置：NAS 导入镜像操作截图 -->
   <!-- 建议截图：绿联云 NAS Docker 管理界面，点击"导入镜像"的操作步骤 -->

   在 NAS 的 Docker 管理界面中，选择"导入镜像"，选择上传的 `.tar` 文件。

4. **创建容器**

   <!-- 📸 截图位置：NAS 创建容器配置截图 -->
   <!-- 建议截图：创建容器时的端口映射和文件夹挂载配置 -->

   配置说明：
   | 配置项 | 值 | 说明 |
   |--------|-----|------|
   | 端口映射 | `7301:7301` | 容器端口映射到主机 |
   | 文件夹挂载 | `/你的音乐目录` → `/app/music` | 挂载你的音乐文件夹 |
   | 文件夹挂载 | `/持久化目录` → `/app/data` | 保存刮削数据 |

---

## 📖 使用指南

### 1️⃣ 浏览音乐文件

<!-- 📸 截图位置：文件浏览操作截图 -->
<!-- 建议截图：点击目录进入子文件夹的操作 -->

1. 打开首页，点击 **"浏览文件"** 卡片
2. 导航到包含音乐文件的目录
3. 点击音乐文件可查看当前元数据

### 2️⃣ 手动刮削单首歌曲

<!-- 📸 截图位置：手动刮削操作流程截图 -->
<!-- 建议截图：选择歌曲 → 搜索 → 选择匹配项 → 确认写入 的完整流程 -->

1. 在文件浏览中选择一首歌曲
2. 点击 **"刮削"** 按钮
3. 选择数据源（华语歌曲推荐企鹅或云村）
4. 从搜索结果中选择正确的匹配项
5. 勾选要写入的字段（封面、标题、艺术家等）
6. 点击 **"确认写入"**

### 3️⃣ 自动批量刮削

<!-- 📸 截图位置：自动刮削配置截图 -->
<!-- 建议截图：展示数据源选择、字段选择、置信度设置等配置项 -->

1. 打开首页，点击 **"自动刮削"** 卡片
2. 选择要刮削的目录
3. 配置刮削选项：
   - **数据源**：勾选要使用的数据源（支持多选，会自动互补）
   - **字段**：选择要获取的信息（封面、歌词、标题等）
   - **最低置信度**：设置匹配阈值（建议 70%）
   - **跳过已有**：是否跳过已有封面/歌词的文件
4. 点击 **"开始刮削"**

### 4️⃣ 查看刮削历史

<!-- 📸 截图位置：历史记录页截图 -->
<!-- 建议截图：展示刮削历史列表和任务详情 -->

1. 打开首页，点击 **"刮削记录"** 卡片
2. 查看历史刮削任务和结果
3. 可以查看每首歌的刮削详情

### 5️⃣ 查看音乐库统计

1. 打开首页，点击 **"音乐库概览"** 卡片
2. 查看元数据完整度、格式分布、刮削覆盖率等统计信息

---

## ⚙️ 配置说明

### 环境变量

| 变量 | 默认值 | 说明 |
|------|--------|------|
| `PORT` | `7301` | 服务端口 |
| `MUSIC_DIR` | `/app/music` | 音乐文件目录 |
| `DATA_DIR` | `/app/data` | 数据存储目录 |
| `TZ` | `UTC` | 时区设置 |

### 封面尺寸设置

在 **设置** 页面可以调整下载封面的最大分辨率：

| 选项 | 说明 |
|------|------|
| 300px | 小封面，节省空间 |
| 500px | 中等封面（推荐） |
| 800px | 大封面，高清显示 |
| 1000px | 超大封面 |

---

## 🔧 支持的音频格式

| 格式 | 元数据支持 | 封面嵌入 | 说明 |
|------|-----------|---------|------|
| MP3 | ✅ ID3v2 | ✅ | 最常见格式 |
| FLAC | ✅ Vorbis | ✅ | 无损格式 |
| M4A/AAC | ✅ MP4 | ✅ | Apple 格式 |
| OGG | ✅ Vorbis | ✅ | 开源格式 |
| WAV | ⚠️ 有限 | ❌ | 建议转换格式 |
| WMA | ✅ ASF | ✅ | Windows 格式 |

---

## 🌐 数据源说明

| 数据源 | 特点 | 推荐场景 |
|--------|------|---------|
| **企鹅音乐** | 华语覆盖全，封面高清 | 华语歌曲首选 |
| **云村音乐** | 华语覆盖好，有歌词 | 华语歌曲备选 |
| **酷狗音乐** | 歌词资源丰富 | 获取歌词 |
| **酷沃音乐** | 曲库较全 | 备用数据源 |
| **苹果音乐** | 欧美日韩覆盖好 | 外语歌曲 |
| **开放数据库** | 开放音乐数据库，数据规范 | 专业用户 |

> 💡 **建议**：勾选多个数据源，系统会自动使用置信度最高的结果，并从其他源补充缺失数据。

---

## ❓ 常见问题

### Q: 刮削后封面没有显示？

**A:** 请检查：
1. 播放器是否支持嵌入式封面
2. 尝试刷新播放器的媒体库
3. 部分老旧播放器需要重启才能识别新封面

### Q: 为什么有些歌曲匹配不到？

**A:** 可能原因：
1. 文件名格式不规范（建议使用"艺术家 - 歌曲名"格式）
2. 歌曲较冷门，数据源没有收录
3. 尝试切换其他数据源或手动搜索

### Q: 刮削速度很慢？

**A:** 为避免被数据源封禁，刮削器会自动限速。批量刮削大量文件时请耐心等待。

### Q: 如何备份刮削数据？

**A:** 备份 `/app/data` 目录（或你挂载的数据卷）即可保存所有刮削记录和设置。

### Q: 支持哪些 NAS 设备？

**A:** 
- ✅ 绿联云 NAS（x86 架构）
- ✅ 群晖 Synology
- ✅ 威联通 QNAP
- ✅ 华硕 ASUS NAS
- ✅ 其他支持 Docker 的 NAS

---

## 📝 更新日志

### v1.0.0 (2025-01)

- 🎉 首个公开发布版本
- ✅ 支持 6 大音乐数据源
- ✅ 智能置信度匹配算法
- ✅ 多源数据互补
- ✅ 批量自动刮削
- ✅ 歌词自动获取
- ✅ 赛博朋克风格 UI
- ✅ 移动端适配
- ✅ Docker 一键部署

---

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

---

## 📄 许可证

[MIT License](LICENSE)

---

## 🙏 致谢

- [Mutagen](https://mutagen.readthedocs.io/) - 音频元数据库
- [Flask](https://flask.palletsprojects.com/) - Web 框架
- 感谢各大音乐平台提供的公开数据

---

<p align="center">
  Made with ❤️ for Music Lovers
</p>

<p align="center">
  如果觉得有用，请给个 ⭐ Star 支持一下！
</p>

