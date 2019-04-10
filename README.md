测试环境 CentOS 7.5 X64
<h3>ssh工具下载</h3>
<a title="" href="https://www.putty.org/" data-original-title="">putty</a>

<a title="" href="https://xshell.en.softonic.com/" data-original-title="">xshell</a>
<h3>连接vps，并安装宝塔面板</h3>
centos
<pre><code>yum install -y wget &amp;&amp; wget -O install.sh http://download.bt.cn/install/install_6.0.sh &amp;&amp; sh install.sh
</code></pre>
ubuntu
<pre><code>wget -O install.sh http://download.bt.cn/install/install-ubuntu_6.0.sh &amp;&amp; sudo bash install.sh
</code></pre>
debian
<pre><code>wget -O install.sh http://download.bt.cn/install/install-ubuntu_6.0.sh &amp;&amp; bash install.sh
</code></pre>
<img class="alignnone size-medium" src="https://img.alicdn.com/bao/uploaded/i1/O1CN019tgI7k1HIfcjjEGUs_!!2-rate.png" width="605" height="500" />
输入y并回车，进行安装
稍等片刻，安装完成会生成宝塔面板登录地址和账号密码，注意保存<img class="alignnone size-medium" src="https://img.alicdn.com/bao/uploaded/i3/O1CN01jiPBSv1HIfciDYuL2_!!2-rate.png" width="646" height="484" />

登录进去后会让你选择安装环境，安装LNMP环境，注意PHP版本选择7.1。

<img class="alignnone size-medium" src="https://img.alicdn.com/bao/uploaded/i2/O1CN01XHsOx11HIfchrkxwz_!!2-rate.png" width="653" height="411" />

大约等待30分钟(每个人机器性能不一样，有快有慢)
环境安装好后，添加一个站点(首页-网站-添加)，绑定你的域名/ip：

<img class="alignnone size-medium" src="https://img.alicdn.com/bao/uploaded/i2/O1CN01Dci8FY1HIfcjjTuOL_!!2-rate.png" width="1023" height="555" />

记住你的这个站点路径，回到putty/xhell中，进入到你的站点目录内：
<pre><code>cd /www/wwwroot/你的站点域名</code></pre>
下载面板程序
<pre><code>git clone -b master https://github.com/miaocloud/ss-panel-v3-mod_Uim.git tmp &amp;&amp; mv tmp/.git . &amp;&amp; rm -rf tmp &amp;&amp; git reset --hard
</code></pre>
回到宝塔面板中，点击站点设置，添加伪静态规则：
<pre><code>location / {
                        try_files $uri $uri/ /index.php$is_args$args;
                }</code></pre>
<img class="alignnone size-medium" src="https://img.alicdn.com/bao/uploaded/i4/O1CN01NplezW1HIfcfexG1u_!!2-rate.png" width="1172" height="630" />

接着点击网站目录，取消防跨站攻击(open_basedir)并将运行目录改为/public并点击保存

<img class="alignnone size-medium" src="https://img.alicdn.com/bao/uploaded/i2/O1CN01ALxvfb1HIfckLl7C2_!!2-rate.png" width="652" height="544" />

找到你的站点根目录下找到storage目录，点击如图按钮修改权限：<img class="alignnone size-medium" src="https://img.alicdn.com/bao/uploaded/i3/O1CN01DMgwTQ1HIfcffLYhH_!!2-rate.png" width="1307" height="472" />

<img class="alignnone size-medium" src="https://img.alicdn.com/bao/uploaded/i2/O1CN01NyTQSo1HIfcj64Gqo_!!2-rate.png" width="397" height="250" />

在文件中打开sql目录并下载glzjin_all.sql<img class="alignnone size-medium" src="https://img.alicdn.com/bao/uploaded/i2/O1CN01G7caZc1HIfcjlCmrp_!!2-rate.png" width="1334" height="510" />

在下载完成后，点击数据库，并导入所下载的glzjin_all.sql

<img class="alignnone size-medium" src="https://img.alicdn.com/bao/uploaded/i2/O1CN01UsZegz1HIfcj6fCJl_!!2-rate.png" width="604" height="266" /><img class="alignnone size-medium" src="https://tc.233fq.tk/images/2019/04/10/1323a32040768ca05b.png" width="596" height="265" /><img class="alignnone size-medium" src="https://tc.233fq.tk/images/2019/04/10/146e8e90d1445eced5.png" width="605" height="267" />

更改数据库权限为所有人

<img class="alignnone size-medium" src="https://tc.233fq.tk/images/2019/04/10/15f8ca38b756f81ff1.png" width="1340" height="503" />

打开文件，进入config目录，将.config.php.example重命名为.config.php<img class="alignnone size-medium" src="https://tc.233fq.tk/images/2019/04/10/1670811b8b7f849b3b.png" width="1309" height="478" />

填写你的站点名字、域名、数据库地址、数据库名、数据库用户名以及数据库密码：<img class="alignnone size-medium" src="https://tc.233fq.tk/images/2019/04/10/17d8f3a1bd7fd0b789.png" width="887" height="318" />

确认无误后保存，

回到putty/xshell中，并在你的站点根目录内执行下面的命令开始安装依赖
<pre><code>cd /www/wwwroot/你的网站根目录</code></pre>
<pre><code>php composer.phar install
</code></pre>
添加管理员账号
<pre><code>php -n xcat createAdmin
</code></pre>
管理员账号创建完成后，现在来同步一下用户数据：
<pre><code>php xcat syncusers
</code></pre>
回车即可，至此面板安装完成

<img src="https://tc.233fq.tk/images/2019/04/10/AT3lRK96262de34ba36081.png"/>
<img src="https://tc.233fq.tk/images/2019/04/10/AT3QG64c62ed7c2f57bff0.png"/>
