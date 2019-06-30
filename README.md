# locWechat2
全球主机论坛新帖企业微信推送
最终效果

 <img src="https://github.com/bjtest3/locWechat2/blob/master/image/xiaoguo1.jpg" alt="Sample"  width="250" height="140">
 ![创建应用](https://github.com/bjtest3/locWechat2/blob/master/image/xiaoguo2.jpg)

# 介绍
自己去申请企业微信，不依赖于第三方服务公共账号<br>
微信企业号参考了这个大佬文章 https://github.com/kaixin1995/InformationPush

**1、申请企业微信公共账号**
- 申请一个[微信企业号](https://work.weixin.qq.com/)，名字随意，记住企业ID
- 然后点击顶部的应用和小程序，，选择创建应用
  **创建应用**  
  ![创建应用](https://github.com/kaixin1995/InformationPush/blob/master/image/%E5%88%9B%E5%BB%BA%E5%BA%94%E7%94%A8.png)  
- 创建应用后，记住AgentId和Secret
  ![创建应用](https://github.com/kaixin1995/InformationPush/blob/master/image/%E5%BA%94%E7%94%A8id%E8%AE%B0%E5%BD%95.png)
- 修改send.php，在对应的位置填写企业ID、Secret、AgentId。
  分别在代码的6、8、10行修改

  企业微信测试推送:http://域名/send.php?msg=测试提交  

**2、下载以及保存推送新帖脚本**

`下载脚本执行，执行前记得16行修改为你的推送地址`

![创建应用](https://github.com/bjtest3/locWechat2/blob/master/image/%E4%BF%AE%E6%94%B9%E6%8E%A8%E9%80%81%E5%9C%B0%E5%9D%80.png)
```
wget https://raw.githubusercontent.com/bjtest3/locWechat2/master/toWechat.py

pip install beautifulsoup4
pip install js2py
pip install request

python toWechat.py
```

**3、应对特殊意外，用这个脚本守护一下**
```
vi listen.sh
chmod +x listen.sh
```
<br>

```
#!/bin/sh

source /etc/profile
retDesc=`ps -ef | grep "toWechat" | grep -v grep`
retCode=$?
if [ ${retCode} -ne 0 ]; 
    then
    echo "`date` restart" >> /root/wechatlisten.log 
    nohup python /root/toWechat.py & 
else
    echo "server on"
fi
```

**加入到定时任务**
```
crontab -e
*/5 * * * * /root/listen.sh
```
