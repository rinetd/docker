docker-compose常用命令

在第二节中的docker-compose up，这两个容器都是在前台运行的。我们可以指定-d命令以daemon的方式启动容器。除此之外，docker-compose还支持下面参数：
--verbose：输出详细信息
-f 制定一个非docker-compose.yml命名的yaml文件
-p 设置一个项目名称（默认是directory名）
docker-compose的动作包括：
build：构建服务
kill -s SIGINT：给服务发送特定的信号。
logs：输出日志
port：输出绑定的端口
ps：输出运行的容器
pull：pull服务的image
rm：删除停止的容器
run: 运行某个服务，例如docker-compose run web python manage.py shell
start：运行某个服务中存在的容器。
stop:停止某个服务中存在的容器。
up：create + run + attach容器到服务。
scale：设置服务运行的容器数量。例如：docker-compose scale web=2 worker=3
