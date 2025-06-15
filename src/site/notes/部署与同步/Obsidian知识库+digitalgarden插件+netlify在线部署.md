---
{"dg-publish":true,"permalink":"/部署与同步/Obsidian知识库+digitalgarden插件+netlify在线部署/","created":"2025-06-14T21:08:42.665+08:00","updated":"2025-06-15T16:41:27.193+08:00"}
---

参考教程：[Obsidian 最简单的发布分享方式 - 经验分享 - Obsidian 中文论坛](https://forum-zh.obsidian.md/t/topic/19256)

## 1.netlify部署网站
1. 点击[Deploy to Netlify | Create a new project from git | Netlify](https://app.netlify.com/start/deploy?repository=https://github.com/oleeskild/digitalgarden)
2. github授权之后，在 “Repository name” 框中输入一个存放笔记的 Github 仓库名称。或者直接使用默认的 “digitalgarden”（自动创建）。digitalgarden会自动创建这个仓库。
3. done，出现以下页面说明部署成功。
		![](/img/user/前端面试/attachments/Pasted image 20250614211440.png)
4. 点击“Permalink” 就是你的网站，现在还什么都没有，只是一些默认内容。
## 2.安装ob插件
在 Obsidian 插件市场中搜索digitalgarden，下载安装并点击启用即可。
## 3.配置插件
1. 获取 Github 密钥备用。
	点击[New Personal Access Token (Classic)](https://github.com/settings/tokens/new?scopes=repo)，note 输入框随便填一下英文名称，expiration 选 no expiration。往下滑点击 "Generate token"按钮并复制密钥。
	![](/img/user/部署与同步/attachments/Pasted image 20250614212843.png)
2. 打开插件 “Digital Garden” 的配置页面。将之前设置的"Repository name"填入仓库名，username 填入 Github 的用户名，token 填入上面一步获得的密钥。URL 填入网站地址（不喜欢默认的项目名可以更改）。
	注意："Slugify Note URL"的选项关掉，不然只要笔记的路径或笔记本名里面有中文，就无法生成正确的链接地址，导致无法访问发布的笔记。
	
	![](/img/user/部署与同步/attachments/Pasted image 20250614214055.png)
## 4.发布笔记
打开笔记页面，搜索并打开命令 “Digital Garden: Quick Publish And Share Note”，笔记就发布好啦，并且自动将页面链接复制到剪贴板上，过一会在浏览器打开链接就可以看到发布好的页面。
![](/img/user/部署与同步/attachments/Pasted image 20250614215532.png)