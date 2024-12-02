2024年12月2日：
mac上docker部署问题备忘：
docker run --name odoo-postgres -e POSTGRES_USER=odoo -e POSTGRES_PASSWORD=odoo -e POSTGRES_DB=odoo -p 5432:5432 -d postgres:15
docker run -d -p 8069:8069 --name odoo --link odoo-postgres:db -e POSTGRES_USER=odoo -e POSTGRES_PASSWORD=odoo -e POSTGRES_DB=odoo odoo 
进入到odoo容器里，运行命令odoo --db_host 172.17.0.2 --db_port 5432 --db_user odoo --db_password odoo -d odoo -i base --xmlrpc-port=8070
先记下上面重要的结果

当前，所有国内的免费镜像源几乎都失效了，实在不想花精力再去找了，接通外网。。。。。
前面用centos7老掉牙的环境，装了个docker的老版本，各种拉取问题。。。。。，包括中间突然断开等问题。。
笔记本的网速慢，想借助一下服务器的高宽带，奈何服务器操作系统版本也太低，装不上新版的podman或是docker-ce等。。。
笔记本上用vmware装了ubuntu最新版，配上最新的podman，终于可以无阻碍的拉取docker镜像了。。。。
软件系统真是个群体工程，最好保持最新版，不然各种兼容性问题，不胜其烦

也是太坑，初始运行默认的脚本没有初始化数据库，只能自己进到容器里，用另外一个端口启动初始化步骤，完成后关闭，再访问默认的端口就好了

运行过程中查看容器日志，报错error from daemon in stream: Error grabbing logs: invalid character '\x00' looking for beginning of value，需要清理日志文件，使用了
docker logs --tail 0 -f <容器ID或名称> > /dev/null命令后恢复正常



