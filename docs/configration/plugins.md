
配置文件中的 `plugins` 部分对应于插件的配置项，一个插件是一个配置单元，每个单元的基本格式为:

```yaml
pluginName:
    enabled: true/false
    otherConfigrations: xxx
```

`enabled` 即为是否启用插件，所以这里只说明部分插件的特殊配置就可以了。

### xss

+ `ie_feature` 如果此项为 true，则会将一些只能在 IE 环境下复现的漏洞爆出来，小白请不要开。

### baseline 

+ `detect_outdated_ssl_version` 是否检测过期的 SSL 版本, 如果目标启用了 TLS1.1, TLS1.0, SSL3.0 都是会报一个漏洞
+ `detect_http_header_config` 是否检查 header 的配置，主要检查一些安全相关的 http 头有没有确实或错误
+ `detect_cors_header_config` 是否检查 cors 相关的问题
+ `detect_server_error_page` 检查响应是不是一个错误页面, 支持主流框架的错误信息检测
+ `detect_china_id_card_number` 检查响应中有没有身份证号信息
+ `detect_serialization_data_in_params` 检查参数中是否存在序列化数据，支持 java，php，python

### cmd_injection
+ `detect_blind_injection` 是否使用盲打来检查命令注入

### dirscan
+ `dictionary` 配置目录字典, 需要是绝对路径

### sqldet:

+ `error_based_detection` 启用报错注入检测
+ `boolean_based_detection` 启用布尔盲注检测
+ `time_based_detection` 启用时间盲注检测

下面两个选项很危险，开启之后可以增加检测率，但是有破坏数据库数据的可能性，请务必了解工作原理之后再开启
+ `dangerously_use_comment_in_sql` 允许检查注入的时候使用注释
+ `dangerously_use_or_in_sql` 允许检查注入的时候使用 `or`

### brute_force

+ `username_dictionary` 弱口令用户名字典, 需要绝对路径
+ `password_dictionary` 弱口令密码字典, 需要绝对路径

如果没有配置将使用内置字典，约 Top8 用户名和 Top80 密码。配置后将做字典合并，即用户字典的与内置的做合并并去重。

### phantasm

+ `depth` 探测深度, 默认为 1, 即只在 URL 深度为 0, 和深度为 1 时运行该插件（前提是启用了该插件)

    定义 http://example.com/，深度为 0
    定义 http://example.com/a/, 深度为 1
+ `poc` 定义默认启用哪些 POC。支持写内置 poc 名字和本地文件的绝对路径，如:

```yaml
phantasm:
    poc:
    - poc-yaml-activemq-cve-2016-3088
    - /Users/test/1.yml
```
