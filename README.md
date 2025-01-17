功能介绍
=========================
定时自动从豆瓣电影的想看、在看、看过中获取影音信息，然后去PT站自动检索种子，找到最佳资源后按豆瓣电影分类提交到BT下载工具下载。在下载前，会自动检查你的Emby中是否已经存在。
基于此功能机制，还顺带具备了下列功能：
- 将一部刚上映，或者还没上映的电影加入想看，当PT站更新时会第一时间帮你下好，被Emby扫描到后直接观看。
- 对剧集类型的影视资源，如果你正在看一部没更新完的剧，只要pt站更新，也会帮你对比本地影音库缺少的剧集开始自动下载。

**注意，豆瓣和PT的读取和检索，均未使用OpenAPI（如有任何合规问题请及时联系作者下架源码），但模拟请求的过程中，增加了随机延迟机制来保护网站。本工具只能用于学习和自己研究，禁止用作任何商业用途！**

环境要求
=========================
- 影视剧集管理服务器：Emby or Jellyfin
- BT下载工具：qbittorrent
- 你需要拥有一个PT站的账号：MTeam（当前仅支持mteam种子自动检索）

如果你恰好是上面的影音方案，就可以直接开始使用了。

部署方式
=========================
- 本应用支持Docker形式启动，日常运行占资源非常低，无CPU消耗（linux crontab调度任务），常驻内存2MB左右；但因为使用了非OpenAPI的形式，所以没有提供打包好的docker镜像进行分享，请自行通过Dockerfile打包；
- 当然也可以下载源码，直接用NAS的定时任务运行，或者你的任何能够定时调度python程序的工具；

源码运行方式请先安装依赖：pip install -r requirements.txt

然后在执行命令：python3 douban_movie_download.py -w /workdir

配置文件
=========================
通过任何形式第一次运行应用时，都会在你指定的工作目录帮助创建一个user_config.yml文件，当然你也可以按源码的doc/user_config.yml模版提前创建，在这个文件中描述了很多注释讲解配置方式。

更多帮助
=========================
如果你在使用过程中有任何问题，或者有其他特殊需求，可以联络我交流，但因为个人精力的关系，我不可能及时回答和解决每个人的问题。

制作成Docker(在项目根目录下运行)
=========================
制作镜像 docker build -t movie_robot . -f Dockerfile --platform linux/amd64 查看镜像 docker images 运行镜像 docker run -it -v -v data:/放置user_config.yml的路径 movie_robot