#docker
一、docker 的安装
1.docker和wsl安装包在本地 【网盘地址】
2.配置阿里云加速器到docker engine
	i 登录阿里云->控制台->搜索容器镜像服务-镜像加速 【网站】
3.下载可视化界面portainer镜像
	i 查看镜像(命令行执行) docker search portainer
	ii 下载镜像(第一个) docker pull portainer/portainer
4. 利用portainer镜像生成portainer容器(以下代码在同一行命令行实现)
	i docker run -d -p 9000:9000 --restart=always 
	-v /var/run/docker.sock:/var/run/docker.sock 
	--name portainer \portainer/portainer
5.Portainer可视化界面使用
	i 本地接口打开 http://localhost:9000

二、Neo4j安装与部署(指令均在命令行执行)
1.获取Neo4j官方镜像
	i 创建最新版本: dokcer pull neo4j
	ii 创建指定版本: docker pull neo4j:3.5
2.创建容器，开启neo4j
	i 创建一个动态运行的独立环境下的neo4j
		docker run --name neo4j_movie neo4j
	ii 设置端口映射(实现同时多开)
		a 容器端口和本机端口映射一致
			docker run --name project1-d -p 7474:7474 -p 7687:7687 neo4j
			本机访问neo4j的http端口: http://localhost:7474
			本机在http页面中 connect url选择neo4j//localhost:7687
		b 修改宿主机端口，映射到docker端口，避免发生冲突
			docker run --name project2 -d -p 7475:7474 -p 7688:7687 neo4j
			访问neo4j的http端口: http://localhost:7475
			本机在http页面中 connect url选择neo4j//localhost:7688

三、docker语法
1.获取镜像
	i docker pull ubuntu
	ii docker pull neo4j:3.5
2.新建容器
	i docker run --name project3 -d -p 7476:7474 -p 7689:7687 neo4j:3.5
		a 运行一个容器： docker run
		b 命名：--name 名称
		c 后台方式运行：-d
		d 宿主机到容器的port映射：-p 宿主机端口:容器端口
		e 运行指定镜像：neo4j:3.5
	ii docker run ubuntu:15.10 /bin/echo "Hello world"
		a 在启动的ubuntu容器中执行命令：/bin/echo "Hello world"
3.对容器的操作
	i 启动已有容器
		docker start 容器名称/id
	ii 关闭已有容器
		docker stop 容器名称/id
	iii 重启容器
		docker restart 容器名称/id
	iv 查看所有容器
		docker ps
	v 导出容器
		(a) docker export 容器id > neo4j.tar
			(neo4j.tar是导出的文件名和文件格式)
		(b) 导出容器中的某个数据
			neo4j_v
	vi 导入容器
		cat docker/neo4j.tar | docker import - test/neo4j

docker run -v /neo4j/data:/data --name movie2 -d -p 7476:7474 -p 7689:7687 -it neo4j /bin/bash




