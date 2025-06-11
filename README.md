# HTTP/HTTPS代理转发器

[![版本](https://img.shields.io/badge/版本-2.0.0-blue.svg)](https://github.com/kk12-30/proxy_forwarder)
[![Python](https://img.shields.io/badge/Python-3.6+-green.svg)](https://www.python.org/)
[![许可证](https://img.shields.io/badge/许可证-MIT-yellow.svg)](LICENSE)

一个灵活的HTTP/HTTPS代理转发工具，支持流量复制、白名单过滤和Burp Suite集成，专为安全测试设计。

## 功能特性

- **流量复制模式**：将请求同时发送到目标服务器和安全扫描器，不影响正常访问
- **白名单过滤**：只转发特定域名/IP的流量到安全扫描器
- **支持HTTP和HTTPS**：完整处理HTTP和HTTPS流量转发
- **Burp Suite集成**：作为Burp Suite和安全扫描器之间的桥梁
- **统计报告**：提供请求数量、转发次数等统计信息
- **灵活配置**：支持命令行参数和配置文件



## 使用方法

### 基本用法

```bash
python proxy_forwarder.py -l 127.0.0.1:8080 -u 127.0.0.1:7777
```

### 参数说明

| 参数                   | 描述                                                 |
| ---------------------- | ---------------------------------------------------- |
| `-l, --listen`         | 监听地址和端口 (默认: 127.0.0.1:8080)                |
| `-u, --upstream`       | 上游代理/扫描器地址和端口 (例如: 127.0.0.1:7777)     |
| `-d, --downstream`     | 下游代理地址和端口 (可选)                            |
| `-w, --whitelist`      | 白名单域名或IP列表 (例如: *.example.com 192.168.1.1) |
| `-f, --whitelist-file` | 从文件加载白名单，每行一个域名或IP                   |
| `-q, --quiet`          | 安静模式，减少输出信息                               |
| `--burp-mode`          | Burp Suite集成模式                                   |
| `--help-usage`         | 显示详细的使用帮助                                   |

### 常见使用场景

#### 1. 作为独立代理

```bash
python proxy_forwarder.py -l 127.0.0.1:8080 -u 127.0.0.1:7777 -w example.com
```

#### 2. 与Burp Suite集成

a) 运行代理转发器:

```bash
python proxy_forwarder.py -l 127.0.0.1:8080 -u 127.0.0.1:7777 -w example.com --burp-mode
```

b) 在Burp Suite中配置(User options -> Connections -> Downstream Proxy Servers):

- 目标主机: *
- 代理主机: 127.0.0.1
- 代理端口: 8080

c) 浏览器设置代理为Burp Suite(默认8080端口)

d) 工作流: 浏览器 -> Burp Suite -> 代理转发器 -> 目标站点 + Xray(被动扫描模式)

### 白名单文件格式

白名单文件中每行包含一个域名或IP，支持以下格式:

```
example.com
*.test.com
192.168.1.1
10.0.0.0/24
```




