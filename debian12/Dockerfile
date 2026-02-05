# 基于Debian 12 (bookworm) slim版本构建，amd64架构
FROM debian:bookworm-slim

# 注释：构建上下文信息（debian.sh脚本参数）
# debian.sh --arch 'amd64' out/ 'bookworm' '@1759104000'

# 设置核心环境变量
ENV DOTNET_RUNNING_IN_CONTAINER=true \
    DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=false \
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
    && rm -rf /var/lib/apt/lists/*

RUN /bin/sh -c curl -fsSL https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor -o /usr/share/keyrings/microsoft-prod.gpg \
&& echo "deb [arch=amd64 signed-by=/usr/share/keyrings/microsoft-prod.gpg] https://packages.microsoft.com/debian/12/prod bookworm main" > /etc/apt/sources.list.d/microsoft.list

# 3. 安装.NET 8.0.20 ASP.NET Core运行时（现在能正常找到包）
RUN /bin/sh -c apt-get update \
    && apt-get install -y --no-install-recommends \
        aspnetcore-runtime-8.0.20 \
    && rm -rf /var/lib/apt/lists/*
# 创建工作目录
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