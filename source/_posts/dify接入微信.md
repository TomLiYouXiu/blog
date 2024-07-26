---
title: dify接入微信
date: 2024-05-14 11:04:41
tags: 教程
categories: Dify
thumbnail: "https://pic.imgdb.cn/item/663c472f0ea9cb1403e4c285.png"
---

# 一、Dify简介



**项目官网**：[Dify.AI · 生成式 AI 应用创新引擎](https://dify.ai/zh)

**Dify** 是一款开源的大语言模型(LLM) 应用开发平台。它融合了后端即服务（Backend as Service）和 [LLMOps](https://docs.dify.ai/v/zh-hans/learn-more/extended-reading/what-is-llmops) 的理念，使开发者可以快速搭建生产级的生成式 AI 应用。即使你是非技术人员，也能参与到 AI 应用的定义和数据运营过程中。

由于 Dify 内置了构建 LLM 应用所需的关键技术栈，包括对数百个模型的支持、直观的 Prompt 编排界面、高质量的 RAG 引擎以及灵活的 Agent 框架，并同时提供了一套易用的界面和 API。这为开发者节省了许多重复造轮子的时间，使其可以专注在创新和业务需求上。

### 为什么使用 Dify？

你或许可以把 LangChain 这类的开发库（Library）想象为有着锤子、钉子的工具箱。与之相比，Dify 提供了更接近生产需要的完整方案，Dify 好比是一套脚手架，并且经过了精良的工程设计和软件测试。

重要的是，Dify 是**开源**的，它由一个专业的全职团队和社区共同打造。你可以基于任何模型自部署类似 Assistants API 和 GPTs 的能力，在灵活的安全的基础上，同时保持对数据的完全控制。

> 我们的社区用户对 Dify 的产品评价可以归结为简单、克制、迭代迅速。 ——路宇，Dify.AI CEO

希望以上信息和这份指南可以帮助你了解这款产品，我们相信 Dify 是为你而做的（Do It For You）。

### Dify 能做什么？



Dify 一词源自 Define + Modify，意指定义并且持续的改进你的 AI 应用，它是为你而做的（Do it for you）。

- **创业**，快速的将你的 AI 应用创意变成现实，无论成功和失败都需要加速。在真实世界，已经有几十个团队通过 Dify 构建 MVP（最小可用产品）获得投资，或通过 POC（概念验证）赢得了客户的订单。
- **将 LLM 集成至已有业务**，通过引入 LLM 增强现有应用的能力，接入 Dify 的 RESTful API 从而实现 Prompt 与业务代码的解耦，在 Dify 的管理界面是跟踪数据、成本和用量，持续改进应用效果。
- **作为企业级 LLM 基础设施**，一些银行和大型互联网公司正在将 Dify 部署为企业内的 LLM 网关，加速 GenAI 技术在企业内的推广，并实现中心化的监管。
- **探索 LLM 的能力边界**，即使你是一个技术爱好者，通过 Dify 也可以轻松的实践 Prompt 工程和 Agent 技术，在 GPTs 推出以前就已经有超过 60,000 开发者在 Dify 上创建了自己的第一个应用。

![image-9jkv.png](https://s3.langlangy.com/langlangyblog/image-9jkv.png)

# 二、Dify on WeChat

**项目地址**：https://github.com/hanfangyuan4396/dify-on-wechat.git

项目为 [chatgpt-on-wechat](https://github.com/zhayujie/chatgpt-on-wechat)下游分支

额外对接了LLMOps平台 [Dify](https://github.com/langgenius/dify)，支持Dify智能助手模型，调用工具和知识库，支持Dify工作流。

如果作者的项目对您有帮助请帮助作者点一个star吧~

![image-95t6.png](https://s3.langlangy.com/langlangyblog/image-95t6.png)

# 三、部署

## 前期准备

首先需要一台服务器，推荐浪浪云服务器：高防，稳定，有保障！！！

浪浪云限时活动推荐：

* [公益免费大模型接口--无需再为api付费 | 浪浪云技术栈 (langlangy.com)](https://blog.langlangy.com/archives/apifree)
* [浪浪云白嫖服务器活动 | 浪浪云技术栈 (langlangy.com)](https://blog.langlangy.com/archives/bphd)

### Dify的搭建：

1.可以参考官方的教程：

2.如果不想这么麻烦的话可以使用浪浪云的一键部署[Dify知识库可接入全场大模型【一.搭建演示篇】 | 浪浪云技术栈 (langlangy.com)](https://blog.langlangy.com/archives/dify)

![image-fe3n.png](https://s3.langlangy.com/langlangyblog/image-fe3n.png)

### 升级Dify版本

购买完浪浪云的服务器后可能会出现Dify的版本较低，此时我们升级版本即可

1.远程连接浪浪云服务器[Linux服务器登陆教程 - 浪浪云：提供高性能、可靠稳定的云服务器解决方案 (langlangy.com)](https://langlangy.com/news/detail/support/9)

2.挨个执行命令

~~~bash
# 进入对应的目录
cd #返回根目录
cd dify/docker/ #进入对应的文件夹
vi docker-compose.yaml #编辑对应的文件信息，或者删除文件，新建也可
docker compose down #停止容器
docker compose pull #拉取新的镜像
docker compose up -d #启动容器
~~~

**docker-compose.yaml**文件内容，可能存在一定的时效性，目前2024年5月8日13:59:54[处于最新版]，也可到项目的官网进行复制对应的文件

~~~yaml
version: '3'
services:
  # API service
  api:
    image: langgenius/dify-api:0.6.6
    restart: always
    environment:
      # Startup mode, 'api' starts the API server.
      MODE: api
      # The log level for the application. Supported values are `DEBUG`, `INFO`, `WARNING`, `ERROR`, `CRITICAL`
      LOG_LEVEL: INFO
      # A secret key that is used for securely signing the session cookie and encrypting sensitive information on the database. You can generate a strong key using `openssl rand -base64 42`.
      SECRET_KEY: sk-9f73s3ljTXVcMT3Blb3ljTqtsKiGHXVcMT3BlbkFJLK7U
      # The base URL of console application web frontend, refers to the Console base URL of WEB service if console domain is
      # different from api or web app domain.
      # example: http://cloud.dify.ai
      CONSOLE_WEB_URL: ''
      # Password for admin user initialization.
      # If left unset, admin user will not be prompted for a password when creating the initial admin account.
      INIT_PASSWORD: ''
      # The base URL of console application api server, refers to the Console base URL of WEB service if console domain is
      # different from api or web app domain.
      # example: http://cloud.dify.ai
      CONSOLE_API_URL: ''
      # The URL prefix for Service API endpoints, refers to the base URL of the current API service if api domain is
      # different from console domain.
      # example: http://api.dify.ai
      SERVICE_API_URL: ''
      # The URL prefix for Web APP frontend, refers to the Web App base URL of WEB service if web app domain is different from
      # console or api domain.
      # example: http://udify.app
      APP_WEB_URL: ''
      # File preview or download Url prefix.
      # used to display File preview or download Url to the front-end or as Multi-model inputs;
      # Url is signed and has expiration time.
      FILES_URL: ''
      # When enabled, migrations will be executed prior to application startup and the application will start after the migrations have completed.
      MIGRATION_ENABLED: 'true'
      # The configurations of postgres database connection.
      # It is consistent with the configuration in the 'db' service below.
      DB_USERNAME: postgres
      DB_PASSWORD: difyai123456
      DB_HOST: db
      DB_PORT: 5432
      DB_DATABASE: dify
      # The configurations of redis connection.
      # It is consistent with the configuration in the 'redis' service below.
      REDIS_HOST: redis
      REDIS_PORT: 6379
      REDIS_USERNAME: ''
      REDIS_PASSWORD: difyai123456
      REDIS_USE_SSL: 'false'
      # use redis db 0 for redis cache
      REDIS_DB: 0
      # The configurations of celery broker.
      # Use redis as the broker, and redis db 1 for celery broker.
      CELERY_BROKER_URL: redis://:difyai123456@redis:6379/1
      # Specifies the allowed origins for cross-origin requests to the Web API, e.g. https://dify.app or * for all origins.
      WEB_API_CORS_ALLOW_ORIGINS: '*'
      # Specifies the allowed origins for cross-origin requests to the console API, e.g. https://cloud.dify.ai or * for all origins.
      CONSOLE_CORS_ALLOW_ORIGINS: '*'
      # CSRF Cookie settings
      # Controls whether a cookie is sent with cross-site requests,
      # providing some protection against cross-site request forgery attacks
      #
      # Default: `SameSite=Lax, Secure=false, HttpOnly=true`
      # This default configuration supports same-origin requests using either HTTP or HTTPS,
      # but does not support cross-origin requests. It is suitable for local debugging purposes.
      #
      # If you want to enable cross-origin support,
      # you must use the HTTPS protocol and set the configuration to `SameSite=None, Secure=true, HttpOnly=true`.
      #
      # The type of storage to use for storing user files. Supported values are `local` and `s3` and `azure-blob` and `google-storage`, Default: `local`
      STORAGE_TYPE: local
      # The path to the local storage directory, the directory relative the root path of API service codes or absolute path. Default: `storage` or `/home/john/storage`.
      # only available when STORAGE_TYPE is `local`.
      STORAGE_LOCAL_PATH: storage
      # The S3 storage configurations, only available when STORAGE_TYPE is `s3`.
      S3_ENDPOINT: 'https://xxx.r2.cloudflarestorage.com'
      S3_BUCKET_NAME: 'difyai'
      S3_ACCESS_KEY: 'ak-difyai'
      S3_SECRET_KEY: 'sk-difyai'
      S3_REGION: 'us-east-1'
      # The Azure Blob storage configurations, only available when STORAGE_TYPE is `azure-blob`.
      AZURE_BLOB_ACCOUNT_NAME: 'difyai'
      AZURE_BLOB_ACCOUNT_KEY: 'difyai'
      AZURE_BLOB_CONTAINER_NAME: 'difyai-container'
      AZURE_BLOB_ACCOUNT_URL: 'https://<your_account_name>.blob.core.windows.net'
      # The Google storage configurations, only available when STORAGE_TYPE is `google-storage`.
      GOOGLE_STORAGE_BUCKET_NAME: 'yout-bucket-name'
      GOOGLE_STORAGE_SERVICE_ACCOUNT_JSON_BASE64: 'your-google-service-account-json-base64-string'
      # The type of vector store to use. Supported values are `weaviate`, `qdrant`, `milvus`, `relyt`.
      VECTOR_STORE: weaviate
      # The Weaviate endpoint URL. Only available when VECTOR_STORE is `weaviate`.
      WEAVIATE_ENDPOINT: http://weaviate:8080
      # The Weaviate API key.
      WEAVIATE_API_KEY: WVF5YThaHlkYwhGUSmCRgsX3tD5ngdN8pkih
      # The Qdrant endpoint URL. Only available when VECTOR_STORE is `qdrant`.
      QDRANT_URL: http://qdrant:6333
      # The Qdrant API key.
      QDRANT_API_KEY: difyai123456
      # The Qdrant client timeout setting.
      QDRANT_CLIENT_TIMEOUT: 20
      # The Qdrant client enable gRPC mode.
      QDRANT_GRPC_ENABLED: 'false'
      # The Qdrant server gRPC mode PORT.
      QDRANT_GRPC_PORT: 6334
      # Milvus configuration Only available when VECTOR_STORE is `milvus`.
      # The milvus host.
      MILVUS_HOST: 127.0.0.1
      # The milvus host.
      MILVUS_PORT: 19530
      # The milvus username.
      MILVUS_USER: root
      # The milvus password.
      MILVUS_PASSWORD: Milvus
      # The milvus tls switch.
      MILVUS_SECURE: 'false'
      # relyt configurations
      RELYT_HOST: db
      RELYT_PORT: 5432
      RELYT_USER: postgres
      RELYT_PASSWORD: difyai123456
      RELYT_DATABASE: postgres
      # Mail configuration, support: resend, smtp
      MAIL_TYPE: ''
      # default send from email address, if not specified
      MAIL_DEFAULT_SEND_FROM: 'YOUR EMAIL FROM (eg: no-reply <no-reply@dify.ai>)'
      SMTP_SERVER: ''
      SMTP_PORT: 587
      SMTP_USERNAME: ''
      SMTP_PASSWORD: ''
      SMTP_USE_TLS: 'true'
      # the api-key for resend (https://resend.com)
      RESEND_API_KEY: ''
      RESEND_API_URL: https://api.resend.com
      # The DSN for Sentry error reporting. If not set, Sentry error reporting will be disabled.
      SENTRY_DSN: ''
      # The sample rate for Sentry events. Default: `1.0`
      SENTRY_TRACES_SAMPLE_RATE: 1.0
      # The sample rate for Sentry profiles. Default: `1.0`
      SENTRY_PROFILES_SAMPLE_RATE: 1.0
      # Notion import configuration, support public and internal
      NOTION_INTEGRATION_TYPE: public
      NOTION_CLIENT_SECRET: you-client-secret
      NOTION_CLIENT_ID: you-client-id
      NOTION_INTERNAL_SECRET: you-internal-secret
      # The sandbox service endpoint.
      CODE_EXECUTION_ENDPOINT: "http://sandbox:8194"
      CODE_EXECUTION_API_KEY: dify-sandbox
      CODE_MAX_NUMBER: 9223372036854775807
      CODE_MIN_NUMBER: -9223372036854775808
      CODE_MAX_STRING_LENGTH: 80000
      TEMPLATE_TRANSFORM_MAX_LENGTH: 80000
      CODE_MAX_STRING_ARRAY_LENGTH: 30
      CODE_MAX_OBJECT_ARRAY_LENGTH: 30
      CODE_MAX_NUMBER_ARRAY_LENGTH: 1000
    depends_on:
      - db
      - redis
    volumes:
      # Mount the storage directory to the container, for storing user files.
      - ./volumes/app/storage:/app/api/storage
    # uncomment to expose dify-api port to host
    # ports:
    #   - "5001:5001"

  # worker service
  # The Celery worker for processing the queue.
  worker:
    image: langgenius/dify-api:0.6.6
    restart: always
    environment:
      # Startup mode, 'worker' starts the Celery worker for processing the queue.
      MODE: worker

      # --- All the configurations below are the same as those in the 'api' service. ---

      # The log level for the application. Supported values are `DEBUG`, `INFO`, `WARNING`, `ERROR`, `CRITICAL`
      LOG_LEVEL: INFO
      # A secret key that is used for securely signing the session cookie and encrypting sensitive information on the database. You can generate a strong key using `openssl rand -base64 42`.
      # same as the API service
      SECRET_KEY: sk-9f73s3ljTXVcMT3Blb3ljTqtsKiGHXVcMT3BlbkFJLK7U
      # The configurations of postgres database connection.
      # It is consistent with the configuration in the 'db' service below.
      DB_USERNAME: postgres
      DB_PASSWORD: difyai123456
      DB_HOST: db
      DB_PORT: 5432
      DB_DATABASE: dify
      # The configurations of redis cache connection.
      REDIS_HOST: redis
      REDIS_PORT: 6379
      REDIS_USERNAME: ''
      REDIS_PASSWORD: difyai123456
      REDIS_DB: 0
      REDIS_USE_SSL: 'false'
      # The configurations of celery broker.
      CELERY_BROKER_URL: redis://:difyai123456@redis:6379/1
      # The type of storage to use for storing user files. Supported values are `local` and `s3` and `azure-blob`, Default: `local`
      STORAGE_TYPE: local
      STORAGE_LOCAL_PATH: storage
      # The S3 storage configurations, only available when STORAGE_TYPE is `s3`.
      S3_ENDPOINT: 'https://xxx.r2.cloudflarestorage.com'
      S3_BUCKET_NAME: 'difyai'
      S3_ACCESS_KEY: 'ak-difyai'
      S3_SECRET_KEY: 'sk-difyai'
      S3_REGION: 'us-east-1'
      # The Azure Blob storage configurations, only available when STORAGE_TYPE is `azure-blob`.
      AZURE_BLOB_ACCOUNT_NAME: 'difyai'
      AZURE_BLOB_ACCOUNT_KEY: 'difyai'
      AZURE_BLOB_CONTAINER_NAME: 'difyai-container'
      AZURE_BLOB_ACCOUNT_URL: 'https://<your_account_name>.blob.core.windows.net'
      # The type of vector store to use. Supported values are `weaviate`, `qdrant`, `milvus`, `relyt`.
      VECTOR_STORE: weaviate
      # The Weaviate endpoint URL. Only available when VECTOR_STORE is `weaviate`.
      WEAVIATE_ENDPOINT: http://weaviate:8080
      # The Weaviate API key.
      WEAVIATE_API_KEY: WVF5YThaHlkYwhGUSmCRgsX3tD5ngdN8pkih
      # The Qdrant endpoint URL. Only available when VECTOR_STORE is `qdrant`.
      QDRANT_URL: http://qdrant:6333
      # The Qdrant API key.
      QDRANT_API_KEY: difyai123456
      # The Qdrant clinet timeout setting.
      QDRANT_CLIENT_TIMEOUT: 20
      # The Qdrant client enable gRPC mode.
      QDRANT_GRPC_ENABLED: 'false'
      # The Qdrant server gRPC mode PORT.
      QDRANT_GRPC_PORT: 6334
      # Milvus configuration Only available when VECTOR_STORE is `milvus`.
      # The milvus host.
      MILVUS_HOST: 127.0.0.1
      # The milvus host.
      MILVUS_PORT: 19530
      # The milvus username.
      MILVUS_USER: root
      # The milvus password.
      MILVUS_PASSWORD: Milvus
      # The milvus tls switch.
      MILVUS_SECURE: 'false'
      # Mail configuration, support: resend
      MAIL_TYPE: ''
      # default send from email address, if not specified
      MAIL_DEFAULT_SEND_FROM: 'YOUR EMAIL FROM (eg: no-reply <no-reply@dify.ai>)'
      # the api-key for resend (https://resend.com)
      RESEND_API_KEY: ''
      RESEND_API_URL: https://api.resend.com
      # relyt configurations
      RELYT_HOST: db
      RELYT_PORT: 5432
      RELYT_USER: postgres
      RELYT_PASSWORD: difyai123456
      RELYT_DATABASE: postgres
      # Notion import configuration, support public and internal
      NOTION_INTEGRATION_TYPE: public
      NOTION_CLIENT_SECRET: you-client-secret
      NOTION_CLIENT_ID: you-client-id
      NOTION_INTERNAL_SECRET: you-internal-secret
    depends_on:
      - db
      - redis
    volumes:
      # Mount the storage directory to the container, for storing user files.
      - ./volumes/app/storage:/app/api/storage

  # Frontend web application.
  web:
    image: langgenius/dify-web:0.6.6
    restart: always
    environment:
      # The base URL of console application api server, refers to the Console base URL of WEB service if console domain is
      # different from api or web app domain.
      # example: http://cloud.dify.ai
      CONSOLE_API_URL: ''
      # The URL for Web APP api server, refers to the Web App base URL of WEB service if web app domain is different from
      # console or api domain.
      # example: http://udify.app
      APP_API_URL: ''
      # The DSN for Sentry error reporting. If not set, Sentry error reporting will be disabled.
      SENTRY_DSN: ''
    # uncomment to expose dify-web port to host
    # ports:
    #   - "3000:3000"

  # The postgres database.
  db:
    image: postgres:15-alpine
    restart: always
    environment:
      PGUSER: postgres
      # The password for the default postgres user.
      POSTGRES_PASSWORD: difyai123456
      # The name of the default postgres database.
      POSTGRES_DB: dify
      # postgres data directory
      PGDATA: /var/lib/postgresql/data/pgdata
    volumes:
      - ./volumes/db/data:/var/lib/postgresql/data
    # uncomment to expose db(postgresql) port to host
    # ports:
    #   - "5432:5432"
    healthcheck:
      test: [ "CMD", "pg_isready" ]
      interval: 1s
      timeout: 3s
      retries: 30

  # The redis cache.
  redis:
    image: redis:6-alpine
    restart: always
    volumes:
      # Mount the redis data directory to the container.
      - ./volumes/redis/data:/data
    # Set the redis password when startup redis server.
    command: redis-server --requirepass difyai123456
    healthcheck:
      test: [ "CMD", "redis-cli", "ping" ]
    # uncomment to expose redis port to host
    # ports:
    #   - "6379:6379"

  # The Weaviate vector store.
  weaviate:
    image: semitechnologies/weaviate:1.19.0
    restart: always
    volumes:
      # Mount the Weaviate data directory to the container.
      - ./volumes/weaviate:/var/lib/weaviate
    environment:
      # The Weaviate configurations
      # You can refer to the [Weaviate](https://weaviate.io/developers/weaviate/config-refs/env-vars) documentation for more information.
      QUERY_DEFAULTS_LIMIT: 25
      AUTHENTICATION_ANONYMOUS_ACCESS_ENABLED: 'false'
      PERSISTENCE_DATA_PATH: '/var/lib/weaviate'
      DEFAULT_VECTORIZER_MODULE: 'none'
      CLUSTER_HOSTNAME: 'node1'
      AUTHENTICATION_APIKEY_ENABLED: 'true'
      AUTHENTICATION_APIKEY_ALLOWED_KEYS: 'WVF5YThaHlkYwhGUSmCRgsX3tD5ngdN8pkih'
      AUTHENTICATION_APIKEY_USERS: 'hello@dify.ai'
      AUTHORIZATION_ADMINLIST_ENABLED: 'true'
      AUTHORIZATION_ADMINLIST_USERS: 'hello@dify.ai'
    # uncomment to expose weaviate port to host
    # ports:
    #  - "8080:8080"

  # The DifySandbox
  sandbox:
    image: langgenius/dify-sandbox:0.1.0
    restart: always
    cap_add:
    # Why is sys_admin permission needed?
    # https://docs.dify.ai/getting-started/install-self-hosted/install-faq#id-16.-why-is-sys_admin-permission-needed
      - SYS_ADMIN
    environment:
      # The DifySandbox configurations
      API_KEY: dify-sandbox
      GIN_MODE: release
      WORKER_TIMEOUT: 15

  # Qdrant vector store.
  # uncomment to use qdrant as vector store.
  # (if uncommented, you need to comment out the weaviate service above,
  # and set VECTOR_STORE to qdrant in the api & worker service.)
  # qdrant:
  #   image: langgenius/qdrant:v1.7.3
  #   restart: always
  #   volumes:
  #     - ./volumes/qdrant:/qdrant/storage
  #   environment:
  #     QDRANT_API_KEY: 'difyai123456'
  #   # uncomment to expose qdrant port to host
  #   # ports:
  #   #  - "6333:6333"
  #   #  - "6334:6334"

  # The nginx reverse proxy.
  # used for reverse proxying the API service and Web service.
  nginx:
    image: nginx:latest
    restart: always
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf
      - ./nginx/proxy.conf:/etc/nginx/proxy.conf
      - ./nginx/conf.d:/etc/nginx/conf.d
      #- ./nginx/ssl:/etc/ssl
    depends_on:
      - api
      - web
    ports:
      - "80:80"
      #- "443:443"
~~~

### 项目Dify on WeChat的拉取与部署（改编自作者大佬的教程）

**创建Dify基础编排聊天助手应用**

登录成功后，进入Dify页面，我们按照下方步骤创建一个基础编排聊天助手应用

![image-os7s.png](https://s3.langlangy.com/langlangyblog/image-os7s.png)

1. 点击页面上方的工作室
2. 创建空白应用
3. 应用类型选择聊天助手
4. 聊天助手编排方式选择基础编排
5. 选择应用图标并为应用填写一个名称，比如基础编排聊天助手
6. 点击创建

Dify的配置较为多样化，也可以参考官方的教程进行个性化配置

在配置完成后，我们可以在右侧对话框进行测试，在测试完成后，进行如下操作

![image-ejuk.png](https://s3.langlangy.com/langlangyblog/image-ejuk.png)

1. 发布
2. 更新
3. 访问API

我们此时就获得到了**api秘钥和服务器地址**

#### Docker进行部署

~~~bash
git clone https://github.com/hanfangyuan4396/dify-on-wechat
cd dify-on-wechat/docker       # 进入docker目录
# 配置dify的API和服务器地址
vi docker-compose.yml
# 我们配置environment字段即可
environment:
      DIFY_API_BASE: '浪浪云ip+对应的端口地址'
      DIFY_API_KEY: 'app-api-key'
      DIFY_APP_TYPE: 'chatbot'
      MODEL: 'dify'
      SINGLE_CHAT_PREFIX: '[""]'
      SINGLE_CHAT_REPLY_PREFIX: '""'
      GROUP_CHAT_PREFIX: '["@bot"]'
      GROUP_NAME_WHITE_LIST: '["ALL_GROUP"]'
# 字段详解
# 
{ 
  "dify_api_base": "https://api.dify.ai/v1",    # dify base url
  "dify_api_key": "app-xxx",                    # dify api key
  "dify_app_type": "chatbot",                   # dify应用类型 chatbot(对应聊天助手)/agent(对应Agent)/workflow(对应工作流)，默认为chatbot
  "dify_convsersation_max_messages": 5,         # dify目前不支持设置历史消息长度，暂时使用超过最大消息数清空会话的策略，缺点是没有滑动窗口，会突然丢失历史消息, 当前为5
  "channel_type": "wx",                         # 通道类型，当前为个人微信
  "model": "dify",                              # 模型名称，当前对应dify平台
  "single_chat_prefix": [""],                   # 私聊时文本需要包含该前缀才能触发机器人回复
  "single_chat_reply_prefix": "",               # 私聊时自动回复的前缀，用于区分真人
  "group_chat_prefix": ["@bot"],                # 群聊时包含该前缀则会触发机器人回复
  "group_name_white_list": ["ALL_GROUP"]        # 机器人回复的群名称列表
}
~~~


~~~bash
docker compose up -d           # 启动docker容器
docker logs -f dify-on-wechat  # 查看二维码并登录
~~~

> 如果作者大佬的项目对您有帮助请帮助大佬点一个star吧~

#### 使用源码部署

~~~bash
#安装依赖
pip3 install -r requirements.txt -i https://mirrors.aliyun.com/pypi/simple
#安装扩展依赖
pip3 install -r requirements-optional.txt -i https://mirrors.aliyun.com/pypi/simple
#复制配置文件
cp config-template.json config.json
#启动
python3 app.py
~~~



### 效果演示

<img src="https://s3.langlangy.com/langlangyblog/1885614c166a66087c38350ae4406d8.jpg" alt="1885614c166a66087c38350ae4406d8.jpg" style="zoom:33%;" />

![81d875498990f4d9e83c89b701b20f1.jpg](https://s3.langlangy.com/langlangyblog/81d875498990f4d9e83c89b701b20f1.jpg)



服务器日志大概如下:

![image-vmd7.png](https://s3.langlangy.com/langlangyblog/image-vmd7.png)

# 四、Q&A

## 有什么问题可以进行提问，常见的问题我会总结为Q&A

# 五、应用案例搭建
