# Kong

## depends_on
虽然 `kong-database` 和 `kong` 这个两个服务是依赖于 `kong-database` 服务的，但是 `depends_on` 并不会按照我们想象的样子执行。
假如需要等待所有依赖的服务都准备就绪后在启动需在使用 compose 的 `Version 2.1` 版本：
**注意在compose 的 `Version 3` 以及 `Version 2` 中 `depends_on` 是不一样的：**
- `condition` 在 `Version 3` 中是不支持的
- 请分别查看 [Version 3 - depends_on](https://docs.docker.com/compose/compose-file/#depends_on) [Version 2 - depends_on](https://docs.docker.com/compose/compose-file/compose-file-v2/#depends_on)

[healthcheck容器健康检查](https://docs.docker.com/compose/compose-file/compose-file-v2/#healthcheck)

## environment
[虽然其格式有以下两种，但是建议使用第一种：](https://docs.docker.com/compose/compose-file/#environment)
```bash
environment:
  RACK_ENV: development
  SHOW: 'true'
  SESSION_SECRET:

environment:
  - RACK_ENV=development
  - SHOW=true
  - SESSION_SECRET
```

## command
[覆盖默认的启动命令](https://docs.docker.com/compose/compose-file/#command)
