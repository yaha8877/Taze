# Taze
{
  "api": {
    "listen": "[::1]:10085",
    "services": [
      "HandlerService",
      "StatsService"
    ],
    "tag": "api"
  },
  "dns": {
    "hosts": {
      "domain:googleapis.cn": "googleapis.com"
    },
    "queryStrategy": "UseIP",
    "servers": [
      "1.1.1.1",
      {
        "address": "1.1.1.1",
        "domains": [],
        "port": 53
      },
      {
        "address": "8.8.8.8",
        "domains": [],
        "port": 53
      }
    ]
  },
  "inbounds": [
    {
      "listen": "127.0.0.1",
      "port": 10808,
      "protocol": "socks",
      "settings": {
        "auth": "noauth",
        "udp": true,
        "userLevel": 8
      },
      "sniffing": {
        "destOverride": [
          "http",
          "tls",
          "quic"
        ],
        "enabled": true
      },
      "tag": "socks"
    },
    {
      "listen": "127.0.0.1",
      "port": 10809,
      "protocol": "http",
      "settings": {
        "userLevel": 8
      },
      "sniffing": {
        "destOverride": [
          "http",
          "tls",
          "quic"
        ],
        "enabled": true
      },
      "tag": "http"
    }
  ],
  "log": {
    "access": "/storage/emulated/0/Android/data/com.happproxy/files/logs/access/access_log.txt",
    "dnsLog": true,
    "error": "/storage/emulated/0/Android/data/com.happproxy/files/logs/error/1758120800598_error_log.txt",
    "loglevel": "debug"
  },
  "outbounds": [
    {
      "mux": {
        "concurrency": -1,
        "enabled": false,
        "xudpConcurrency": 8,
        "xudpProxyUDP443": ""
      },
      "protocol": "vless",
      "settings": {
        "vnext": [
          {
            "address": "151.101.3.6",
            "port": 443,
            "users": [
              {
                "encryption": "none",
                "flow": "",
                "id": "Klent",
                "level": 8,
                "security": "auto"
              }
            ]
          }
        ]
      },
      "streamSettings": {
        "network": "xhttp",
        "security": "tls",
        "tlsSettings": {
          "allowInsecure": true,
          "alpn": [
            "h3"
          ],
          "fingerprint": "chrome",
          "publicKey": "",
          "serverName": "gaharly.xyz",
          "shortId": "",
          "show": false,
          "spiderX": ""
        },
        "xhttpSettings": {
          "host": "gaharly.xyz",
          "mode": "auto",
          "path": "/",
          "scMaxConcurrentPosts": 10,
          "scMaxEachPostBytes": 1000000,
          "scMinPostsIntervalMs": "30"
        }
      },
      "tag": "proxy"
    },
    {
      "protocol": "freedom",
      "tag": "direct"
    },
    {
      "protocol": "blackhole",
      "tag": "block"
    }
  ],
  "policy": {
    "levels": {
      "8": {
        "connIdle": 300,
        "downlinkOnly": 1,
        "handshake": 4,
        "uplinkOnly": 1
      }
    },
    "system": {
      "statsOutboundUplink": true,
      "statsOutboundDownlink": true
    }
  },
  "remarks": "Italy-Klent",
  "routing": {
    "domainStrategy": "IPIfNonMatch",
    "rules": [
      {
        "ip": [
          "1.1.1.1"
        ],
        "outboundTag": "proxy",
        "port": "53"
      },
      {
        "ip": [
          "8.8.8.8"
        ],
        "outboundTag": "direct",
        "port": "53"
      }
    ]
  },
  "stats": {}
}
