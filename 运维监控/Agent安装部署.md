### 安装部署

#### 初始化数据库 

- 连接本地数据库 
  
  IP地址与端口为 127.0.0.1:3306
  
- 执行SQL脚本, 创建数据库

在MySQL数据库中, 执行 /sql/agent.ddl 文件, 创建 dtagent数据库

#### 修改配置文件

```
# logger
log.dir: /tmp/em2.0
log.max-logger-size: 100
log.max-logger-backups: 3
log.days-to-keep: 1

#publish:
#  elasticsearch:
#    hosts: ["http://localhost:9200"]
#    username: ""
#    password: ""
#  influxdb:
#    hosts: ["http://localhost:8086"]
#    username: "admin"
#    password: "admin"
#  transfer:
#    server: localhost
#    port: 8790
#    concurrency: 4    # optional, default 1
#    timeout: 3s       # optional, default 3s
#    cert:             # optional
#    tls:              # optional
#    tls-skip-verify:  # optional
#  kafka:
#    hosts: ["121.43.166.210:9092"]
#    username: ""
#    password: ""
#    timeout: 3s
#  http:
#    host: "127.0.0.1:8864"
#    uri: /api/v2/instance/%s/%s #first %s means agent_id, second %s means type
#    timeout: 30s

publish.http.host: 127.0.0.1:8864
publish.http.uri: /api/v2/instance/%s/%s
publish.http.timeout: 30s

# databases
mysqldb.host: 127.0.0.1
mysqldb.port: 3306
mysqldb.user: root
mysqldb.password: 12345678
mysqldb.dbname: dtagent

#uicdb.host: 127.0.0.1
#uicdb.port: 3306
#uicdb.user: easyagent
#uicdb.password: dtstack
#uicdb.dbname: dtuic

# api
api.port: 8889
api.host:

# rpc
rpc.port: 8890
rpc.cert:
rpc.key:
```


#### 启动服务器

在 build/release/server/darwin-amd64 目录中, 并执行命令：

```
easy-agent-server -c example-config.yml 
```

执行完命令后，控制台显示如下信息

```
Saving logs at /tmp/em2.0
config publish ok!
Running RPC service at 8890
Running API service at 8889
```

表明服务器启动成功。

#### 启动SideCar

在 build/release/sidecar/darwin-amd64 目录中, 并执行命令：

```
sidecar -c example-config.yml 
```

执行完命令后，控制台显示如下信息

```
saving logs at /tmp/
Got Raw buffer: [16]int8{97, 112, 102, 115, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0}
Got Raw buffer: [16]int8{100, 101, 118, 102, 115, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0}
Got Raw buffer: [16]int8{97, 112, 102, 115, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0}
Got Raw buffer: [16]int8{97, 112, 102, 115, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0}
Got Raw buffer: [16]int8{97, 112, 102, 115, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0}
Got Raw buffer: [16]int8{97, 112, 102, 115, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0}
Got Raw buffer: [16]int8{97, 117, 116, 111, 102, 115, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0}
```

表明SideCar启动成功。