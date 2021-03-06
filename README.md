# 使用Fekit数据模拟 #

----------

在做fekit本地vm模拟开发的时候，时常需要与服务端的数据交互，不同开发者有不同的做法，有的直接把url指向到一个静态json文件，联调的时候再改回来，有的要借助第三方软件来实现跳转控制，不管哪种方式都需要很多成本，一两个页如此可能能接受，但长期如此也会让人疲惫。如今fekit自身也能支持数据模拟了，妈妈再也不用担心我的工作了。
## 服务启动 ##

启动 fekit server 时，可以通过读取配置，进行不同的 mock 处理 如: fekit server -p 8083 -m mock.js
>     module.exports={
>     	 rules:[
>     		  {
>     		     pattern:/\/apache\.json/,
>     		     respondwith:'./index.json'
>     		  }
>     	]
>     }


     module.exports=function(){
     $.ajax({
        url:'/apache.json',
        success:backfn,
        dataType:"JSON",
        error:function(msg){
          console.log(msg);
        }
     })
     function backfn(res){
        for(var i=0;i<res.length;i++){
              console.log(res[i].data.title);
              var html="<dl><dt><img src=\""+res[i].data.pic+"\"></dt>"
                html+="<dd>"+res[i].data.title+"</dd></dl>";
                $('.new_dl').append(html);
                 }
        }
 }
## 模拟数据 ##
### apache直接访问json ###

后台数据（模拟）：[http://localhost:8081/apache.json](http://localhost:8081/apache.json "http://localhost:8081/apache.json")

## 存储图片 ##
### 七牛存储 ###
图片1：[http://7xn9on.com1.z0.glb.clouddn.com/tour1.png](http://7xn9on.com1.z0.glb.clouddn.com/tour1.png "http://7xn9on.com1.z0.glb.clouddn.com/tour1.png")

图片1：[http://7xn9on.com1.z0.glb.clouddn.com/tour2.png](http://7xn9on.com1.z0.glb.clouddn.com/tour2.png "http://7xn9on.com1.z0.glb.clouddn.com/tour2.png")

图片1：[http://7xn9on.com1.z0.glb.clouddn.com/tour3.png](http://http://7xn9on.com1.z0.glb.clouddn.com/tour3.png "http://7xn9on.com1.z0.glb.clouddn.com/tour3.png")
## git 命令 ##
### 创建分支 ###
    $ git checkout -b dev
### 查看分支 ###
    $ git branch dev
### 切换分支 ###
    $ git checkout dev
### 删除分支 ###
    $ git branch -d dev
### dev分支的工作成果合并到master分支(当前是master分支) ###
    $ git merge dev
### 查看远程主机 ###
    $ git remote
    $ git remote -v
### 远程删除 ###
    $ git push origin :refs/tags/v0.9
### git fetch取回所有分支（branch）的更新。如果只想取回特定分支的更新，可以指定分支名。 ###
    $ git fetch <远程主机名> <分支名>
	$ git fetch origin master
### 取回origin主机的next分支，与本地的master分支合并（取回origin/next分支，再与当前分支合并。实质上，这等同于先做git fetch，再做git merge） ###
	$ git pull origin next:master
### git push命令用于将本地分支的更新，推送到远程主机 ###
	$ git push origin master