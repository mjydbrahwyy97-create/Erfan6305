{
  "name": "silver-link-5cceab",
  "build": {
    "dockerfile": "Dockerfile",
    "context": "."
  },
  "features": {
    "ghcr.io/devcontainers/features/common-utils:2": {
      "installZsh": false
    },
    "ghcr.io/devcontainers/features/github-cli:1": {
      "version": "latest"
    }
  },
  "postAttachCommand": "gh codespace ports visibility 443:public -c $CODESPACE_NAME && bash /usr/local/bin/start.sh",
  "portsAttributes": {
    "443": {
      "label": "silver-link-5cceab",
      "protocol": "http",
      "onAutoForward": "silent"
    }
  },
  "forwardPorts": [
    443
  ],
  "hostRequirements": {
    "cpus": 2
  }
}
FROM debian:bookworm-slim
COPY setup.sh /tmp/setup.sh
COPY config.json /etc/xray/g2ray.json
COPY show-link.sh /usr/local/bin/show-link.sh
COPY start.sh /usr/local/bin/start.sh
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       bash curl wget unzip ca-certificates openssl uuid-runtime tmux \
    && rm -rf /var/lib/apt/lists/* \
    && mkdir -p /etc/xray \
    && chmod +x /tmp/setup.sh \
    && /tmp/setup.sh \
    && rm /tmp/setup.sh \
    && chmod +x /usr/local/bin/show-link.sh \
    && chmod +x /usr/local/bin/start.sh
EXPOSE 443
CMD ["/usr/local/bin/xray","run","-c","/etc/xray/g2ray.json"]
