### debugger模式
- 1 添加三个必备环境变量
  - CONFIG_PATH=E:\Project\TrendRadar\config\config.yaml; // 配置文件路径
  - FREQUENCY_WORDS_PATH=E:\Project\TrendRadar\config\frequency_words.txt;  //关键词文件路径
  - ENABLE_WEBSERVER=true    //开启html页面生成
- 2 在ide使用debugger模式启动项目 trendradar.__main__.py
- 常用docker命令
```angular2html
# 查看运行状态
docker exec -it trendradar python manage.py status

# 手动执行一次爬虫
docker exec -it trendradar python manage.py run

# 查看实时日志
docker exec -it trendradar python manage.py logs

# 显示当前配置
docker exec -it trendradar python manage.py config

# 显示输出文件
docker exec -it trendradar python manage.py files

# Web 服务器管理（用于浏览器访问生成的报告）
docker exec -it trendradar python manage.py start_webserver   # 启动 Web 服务器
docker exec -it trendradar python manage.py stop_webserver    # 停止 Web 服务器
docker exec -it trendradar python manage.py webserver_status  # 查看 Web 服务器状态

# 查看帮助信息
docker exec -it trendradar python manage.py help

# 重启容器
docker restart trendradar

# 停止容器
docker stop trendradar

# 删除容器（保留数据）
docker rm trendradar
```

- 本地链接mcp json配置
```
 "trendradar": {
      "name": "trendradar",
      "transport": "http",
      "url": "http://localhost:3333/mcp"
    }
```

### 本地自己构建docker镜像
1. cd docker
2. docker compose -f docker-compose-build.yml build
3. 如何存在python版本问题则手动拉取python:  docker pull python:3.11-slim(版本和Dockerfile一致，如果拉取不到则切换其他版本)
4. 拉取python镜像后再执行 docker compose -f docker-compose-build.yml build
5. 创建容器 docker compose -f docker-compose-build.yml up -d   （注意：不要直接使用docker-compose up -d 这样会重新拉取远程镜像）