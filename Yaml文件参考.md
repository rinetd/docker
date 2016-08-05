在上面的yaml文件中，我们可以看到compose文件的基本结构。首先是定义一个服务名，下面是yaml服务中的一些选项条目：
image:镜像的ID
build:直接从pwd的Dockerfile来build，而非通过image选项来pull
links：连接到那些容器。每个占一行，格式为SERVICE[:ALIAS],例如 – db[:database]
external_links：连接到该compose.yaml文件之外的容器中，比如是提供共享或者通用服务的容器服务。格式同links
command：替换默认的command命令
ports: 导出端口。格式可以是：

ports:-"3000"-"8000:8000"-"127.0.0.1:8001:8001"

expose：导出端口，但不映射到宿主机的端口上。它仅对links的容器开放。格式直接指定端口号即可。
volumes：加载路径作为卷，可以指定只读模式：

volumes:-/var/lib/mysql
 - cache/:/tmp/cache
 -~/configs:/etc/configs/:ro

volumes_from：加载其他容器或者服务的所有卷

environment:- RACK_ENV=development
  - SESSION_SECRET

env_file：从一个文件中导入环境变量，文件的格式为RACK_ENV=development
extends:扩展另一个服务，可以覆盖其中的一些选项。一个sample如下：

common.yml
webapp:
  build:./webapp
  environment:- DEBUG=false- SEND_EMAILS=false
development.yml
web:extends:
    file: common.yml
    service: webapp
  ports:-"8000:8000"
  links:- db
  environment:- DEBUG=true
db:
  image: postgres

net：容器的网络模式，可以为”bridge”, “none”, “container:[name or id]”, “host”中的一个。
dns：可以设置一个或多个自定义的DNS地址。
dns_search:可以设置一个或多个DNS的扫描域。
其他的working_dir, entrypoint, user, hostname, domainname, mem_limit, privileged, restart, stdin_open, tty, cpu_shares，和docker run命令是一样的，这些命令都是单行的命令。例如：

cpu_shares:73
working_dir:/code
entrypoint: /code/entrypoint.sh
user: postgresql
hostname: foo
domainname: foo.com
mem_limit:1000000000
privileged:true
restart: always
stdin_open:true
tty:true
