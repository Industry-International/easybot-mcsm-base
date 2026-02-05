# 基于Debian 12 (bookworm) slim版本构建，amd64架构
FROM debian:bookworm-slim

# 注释：构建上下文信息（debian.sh脚本参数）
# debian.sh --arch 'amd64' out/ 'bookworm' '@1759104000'

# 设置核心环境变量
ENV DOTNET_RUNNING_IN_CONTAINER=true \
    DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=true \
    DEBIAN_FRONTEND=noninteractive \
    TZ=Asia/Shanghai

# 安装.NET运行时核心依赖，清理缓存（合并为一层减少镜像体积）
RUN /bin/sh -c apt-get update \
    && apt-get install -y --no-install-recommends \
        ca-certificates \
        libc6 \
        libgcc-s1 \
        libicu72 \
        libssl3 \
        libstdc++6 \
        tzdata \
        zlib1g \
        aspnetcore-runtime-8.0.20 \
    && rm -rf /var/lib/apt/lists/*

# 创建工作目录
RUN mkdir -p /data
WORKDIR /data

# 安装浏览器/无头浏览器核心依赖，清理缓存
RUN /bin/sh -c apt-get update \
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