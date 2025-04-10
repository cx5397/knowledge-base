## 安装

- 安装 node ，v16 及以上版本
- 安装 python ，版本 v3.11.x or v3.12.x
- 安装 docker
- 运行 ankane/pgvector =postgresql+vector

## 配置数据库

- 建库

```
# 在 PostgreSql 中手动创建MaxKB 应用数据库，名称为maxkb
# 创建数据库
CREATE DATABASE "maxkb";
# 切换使用数据库
\c "maxkb";
# 创建vector 扩展
CREATE EXTENSION "vector";
```

- 设置

```
# 将config_example.yml配置文件拷贝至 /opt/maxkb/conf目录下(window为盘符的根目录)
# 配置数据库信息
# 数据库配置（将以下信息替换为实际环境信息）
DB_NAME: maxkb
DB_HOST: localhost
DB_PORT: 5432
DB_USER: root
DB_PASSWORD: xxx
DB_ENGINE: django.db.backends.postgresql_psycopg2

# 模型相关配置
# 模型路径:如果EMBEDDING_MODEL_NAME是绝对路径则无效,反之则会从https://huggingface.co/下载模型到当前目录
EMBEDDING_MODEL_PATH: /opt/maxkb/model/
# 模型名称:如果模型名称是路径,则会加载目录下的模型,如果是模型名称,则会在https://huggingface.co/下载模型 模型的下载位置为EMBEDDING_MODEL_PATH
EMBEDDING_MODEL_NAME: /opt/maxkb/model/shibing624_text2vec-base-chinese
```

## 安装依赖&启动

```
# 前端
cd ui
npm install
npm run dev
# 后端
# 安装 poetry 包管理器
pip install poetry
# 安装后端需要的依赖
poetry install

# 启动项目
poetry run python main.py dev
# 启动模型
poetry run python main.py dev local_model
# 启动异步任务
poetry run python main.py dev celery

或者用poetry shell进入具体虚拟环境(提示还需要安装其他东西)
```

## 默认账号&密码

- admin
- MaxKB@123..
