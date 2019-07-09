# PyProxy-Async
基于 Python 协程 + Redis 实现的简单的代理池维护，及代理 IP 抓取服务

## 流程图
![流程图](https://doc.pjialin.com/stuff/B6LkuGaXEMtItuPtT69CFQ.png)

## Features
* HTTP/HTTPS 检测
* 协程实现
* Web Api 接口支持

## TODO
- [ ] Docker Support
- [ ] TSDB Support
- [ ] More api Support

## Usage
1. 克隆
```
git clone https://github.com/pjialin/pyproxy-async
cd pyproxy-async
```
2. 安装依赖
```
pip install -r requirements.txt 
```
3. 完善配置文件
```
cp config.toml.example config.toml
```
4. 启动
```
python main.py
```

## Web Api
启动完成之后，访问 `127.0.0.1:8080/get_ip` (配置文件中的端口)，即可获得一个随机的 IP, 如
```
# curl http://127.0.0.1:8080/get_ip  
{"ip":"213.6.45.18","port":"39252","http":"http://213.6.45.18:39252"}
# 支持过滤条件 https，如
curl http://127.0.0.1:8080/get_ip?https=1
```

### 从文件中加载已存在的 IP 列表
1. 将文件命名为 `*.ip.txt`，如 `new.ip.txt`，并放在根目录下，文件格式为 `host:port`，如 
```
127.0.0.1:80
127.0.0.1:8080
```
2. 加载到 IP 池中
```
python load.py [file_name]  # 默认加载所有 *.ip.txt 文件
```

### 添加抓取服务
增加新的 IP 抓取服务非常简单，只需要定义好要抓取的页面和对应的解析器，框架会自动加载并进行抓取。
在 `src/sites` 目录中提供了一个示例文件，`site.py.example`，供参考 

## License
[Apache License 2.0](https://github.com/pjialin/pyproxy-async/blob/master/LICENSE)
