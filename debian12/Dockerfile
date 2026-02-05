# 基于Debian 12 (bookworm) slim版本构建，amd64架构
FROM debian:bookworm-slim

# 注释：构建上下文信息（debian.sh脚本参数）
# debian.sh --arch 'amd64' out/ 'bookworm' '@1759104000'

# 设置核心环境变量
ENV DOTNET_RUNNING_IN_CONTAINER=true \
    DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=false \
    DEBIAN_FRONTEND=noninteractive \
    TZ=Asia/Shanghai

# 修复：移除多余的/bin/sh -c，直接执行apt-get命令
# 安装基础依赖 + 添加微软源所需工具（curl/gnupg）
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        ca-certificates \
        libc6 \
        libgcc-s1 \
        libicu72 \
        libssl3 \
        libstdc++6 \
        tzdata \
        zlib1g \
        curl \
        gnupg \
        dotnet-sdk-8.0 \
    && rm -rf /var/lib/apt/lists/*

# 设置工作目录（自动创建/data，无需手动mkdir）
WORKDIR /data

# 安装浏览器/无头浏览器核心依赖（同样移除多余的/bin/sh -c）
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        libappindicator3-1 \
        libasound2 \
        libatk-bridge2.0-0 \
        libatk1.0-0 \
        libcairo2 \
        libcups2 \
        libdbus-1-3 \
        libexpat1 \
        libfontconfig1 \
        libgbm1 \
        libglib2.0-0 \
        libgtk-3-0 \
        libnspr4 \
        libnss3 \
        libpango-1.0-0 \
        libpangocairo-1.0-0 \
        libx11-6 \
        libx11-xcb1 \
        libxcb1 \
        libxcomposite1 \
        libxcursor1 \
        libxdamage1 \
        libxext6 \
        libxfixes3 \
        libxi6 \
        libxrandr2 \
        libxrender1 \
        libxss1 \
        libxtst6 \
        xdg-utils \
        xvfb \
    && rm -rf /var/lib/apt/lists/*


# 容器启动执行的主程序
ENTRYPOINT ["/data/EasyBot"]