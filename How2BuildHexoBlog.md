# Hexo 折腾

Tips：非 Mac 系统肯定不一样，应该就不必参考本文了。[Windows 配置参考](https://github.com/jerry011235/hexoblog/blob/master/source/_posts/windows%E4%B8%8B%E6%90%AD%E5%BB%BAhexo%E5%8D%9A%E5%AE%A2%E5%B9%B6%E5%B0%86%E5%85%B6%E9%83%A8%E7%BD%B2%E5%88%B0GitCafe%E5%92%8CGithub%E7%BB%88%E6%9E%81%E6%95%99%E7%A8%8B.md)

## 思路梳理

1. 配置 Hexo 环境（node.js 和 git）
2. 指定本地文件夹，并安装 Hexo
3. 配置参数
4. 熟悉命令行，本地调试运行
5. git 配置
6. git 与 Github 服务器认证、对接
7. 测试 Github Pages 部署情况
8. 折腾主题

## 操作步骤

1. 安装 Hexo 环境及 Hexo：见 [Hexo 官方文档](https://hexo.io/docs/)
   - 常用命令
     - ```hexo new draft [Blogname]``` 新建草稿
     - ```hexo new [Blogname]``` 直接新建文章
     - ```hexo generate``` 生成 HTML 静态页面，可简写为 ```hexo g```
     - ```hexo deploy```  部署至服务器，可简写为 ```hexo d``` ，连着上一步写作 ```hexo g -d``` 
   - 检查效果 ```hexo server``` ，浏览器打开 ```http://localhost:4000/```  查看效果
2. 文件夹内安装 git
   - 确认已安装 [Git](https://git-scm.com/)
   - ```cd hexo```
   - ```git init``` 
3. git 与 Github 连接
   - [git publickey 认证](http://stackoverflow.com/questions/2643502/git-permission-denied-publickey) & [publickey 拷贝至 Github](https://github.com/ResetSpacetime/zhaochuanyang.github.io/settings/keys) 
     - 思路：获取 key，拷贝至 Github，提交，代码行确认认证
   - 在  Github Repository 的 Code 内创建新的 Branch  ```gh-pages```  （点击 Branch: master ，敲入 ```gh-pages``` ）
4. 部署代码
   - 修改 ```_config.yml```  最好用 https，在  Github Repository 的 Code 内点击 Clone or download -> use https -> copy 链接，填写进 ```_config.yml``` 
     - ```
       deploy:
       	type: git
       	repo: https://github.com/[RepositoryNmae]/XXX.github.io.git
       	branch: gh-pages```
   - ```npm install hexo-deployer-git --save```  安装 git deploy 包
   - ```hexo generate```  生成页面
   - ```hexo deploy``` 部署至 Github
5. 更换主题
   - 我用的：[maupassant-hexo](https://github.com/tufu9441/maupassant-hexo) （含配置方法）
     - ```npm install hexo-renderer-sass --save```  这一步如果报错，需要换为 ```cnpm``` （[淘宝 NPM 镜像](https://npm.taobao.org/) ）：
       - ```npm uninstall  hexo-renderer-sass --save``` 
       - ```npm install -g cnpm --registry=https://registry.npm.taobao.org``` 
       - ```cnpm install hexo-renderer-sass --save``` 
     - 有自己域名的，配置 CNAME 文件（文件名 CNAME 无后缀，内容为指向的域名链接）放入 hexo 下的 source 文件夹，在 DNSPod 上配置解析（日后 favicon.ico、images 也都要放在这里），配置后记得 generate 和 deploy
