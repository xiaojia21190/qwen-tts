# Qwen TTS API

通义千问语音合成 API 客户端和服务器

## 功能特性

- 🎙️ 调用 Qwen TTS 服务进行语音合成
- 🌐 提供 HTTP REST API 接口
- 🎵 支持 50+ 种发音人
- 🌍 支持多种语言（中文、英文、日语、韩语等）
- ⚡ 异步流式处理

## 快速开始

### 1. 安装依赖

```bash
uv sync
```

### 2. 方式一：Docker 部署（推荐）

#### 使用 Docker Compose

```bash
# 启动服务
docker-compose up -d

# 查看日志
docker-compose logs -f

# 停止服务
docker-compose down
```

#### 使用 Docker 命令

```bash
# 构建镜像
docker build -t qwen-tts .

# 运行容器
docker run -d -p 8000:8000 --name qwen-tts qwen-tts

# 查看日志
docker logs -f qwen-tts
```

#### 使用 GitHub Container Registry

```bash
# 拉取镜像
docker pull ghcr.io/jiaws/qwen-tts:latest

# 运行
docker run -d -p 8000:8000 ghcr.io/jiaws/qwen-tts:latest
```

### 方式一：直接调用（Python API）

```python
from main import synthesize

# 合成语音
output = synthesize(
    text="你好，我是通义千问",
    voice="Cherry / 芊悦",
    language="Chinese / 中文",
    output_path="output.wav"
)
print(f"音频已保存到: {output}")
```

### 方式二：启动 API 服务器

```bash
# 启动服务器
python api_server.py
```

服务器将在 `http://localhost:8000` 启动

#### API 端点

| 方法 | 路径 | 描述 |
|------|------|------|
| GET | `/` | API 信息 |
| GET | `/health` | 健康检查 |
| GET | `/voices` | 获取发音人列表 |
| GET | `/languages` | 获取语言列表 |
| POST | `/tts` | 语音合成（JSON） |
| GET | `/tts` | 语音合成（Query） |
| GET | `/audio/{file_id}` | 下载音频 |

#### 示例请求

```bash
# 合成语音
curl -X POST "http://localhost:8000/tts" \
  -H "Content-Type: application/json" \
  -d '{
    "text": "你好，我是通义千问",
    "voice": "Cherry / 芊悦",
    "language": "Chinese / 中文"
  }'

# 或使用 GET
curl "http://localhost:8000/tts?text=你好&voice=Cherry%20/%20芊悦"
```

### 方式三：使用客户端

```bash
# 合成语音
python client_example.py -t "你好，我是通义千问"

# 使用不同发音人
python client_example.py -t "Hello world" -v "Jennifer / 詹妮弗" -l "English / 英文"

# 列出所有发音人
python client_example.py --list-voices
```

## 可用发音人

### 中文发音人
- Cherry / 芊悦
- Serena / 苏瑶
- Ethan / 晨煦
- Chelsie / 千雪
- Momo / 茉兔
- Vivian / 十三
- Moon / 月白
- Maia / 四月
- Kai / 凯
- Bella / 萌宝

### 方言发音人
- Li / 南京-老李
- Marcus / 陕西-秦川
- Roy / 闽南-阿杰
- Peter / 天津-李彼得
- Eric / 四川-程川
- Rocky / 粤语-阿强
- Kiki / 粤语-阿清
- Sunny / 四川-晴儿
- Jada / 上海-阿珍
- Dylan / 北京-晓东

### 精品百人
- Eldric Sage / 精品百人-沧明子
- Mia / 精品百人-乖小妹
- Mochi / 精品百人-沙小弥
- Bellona / 精品百人-燕铮莺
- Vincent / 精品百人-田叔
- Bunny / 精品百人-萌小姬
- Neil / 精品百人-阿闻
- Elias / 墨讲师
- Arthur / 精品百人-徐大爷
- Nini / 精品百人-邻家妹妹
- Ebona / 精品百人-诡婆婆
- Seren / 精品百人-小婉
- Pip / 精品百人-调皮小新
- Stella / 精品百人-美少女阿月

### 外语发音人
- Jennifer / 詹妮弗 (英文)
- Ryan / 甜茶 (英文)
- Katerina / 卡捷琳娜 (英文)
- Aiden / 艾登 (英文)
- Bodega / 西班牙语-博德加
- Alek / 俄语-阿列克
- Dolce / 意大利语-多尔切
- Sohee / 韩语-素熙
- Ono Anna / 日语-小野杏
- Lenn / 德语-莱恩
- Sonrisa / 西班牙语拉美-索尼莎
- Emilien / 法语-埃米尔安
- Andre / 葡萄牙语欧-安德雷
- Radio Gol / 葡萄牙语巴-拉迪奥·戈尔

## 可用语言

- Auto / 自动
- English / 英文
- Chinese / 中文
- German / 德语
- Italian / 意大利语
- Portuguese / 葡萄牙语
- Spanish / 西班牙语
- Japanese / 日语
- Korean / 韩语
- French / 法语
- Russian / 俄语

## 项目结构

```
qwen-tts/
├── main.py                    # 核心 TTS 客户端
├── api_server.py              # FastAPI HTTP 服务器
├── client_example.py          # 客户端示例
├── pyproject.toml             # 项目配置
├── README.md                  # 说明文档
├── Dockerfile                 # Docker 镜像构建
├── docker-compose.yml         # Docker Compose 配置
├── .dockerignore              # Docker 忽略文件
└── .github/
    └── workflows/
        └── docker-build.yml   # GitHub Actions CI/CD
```

## 许可证

MIT License
