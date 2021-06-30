## 检测到目标站点存在JAVASCRIPT框架库漏洞

问题描述：

​	质量安全检测部门，安全渗透检测，查出`有个Javascript 框架漏洞，，主要是把通过框架把涉及XSS跨站的的字符和关键字进行过滤`

原因分析，**cookie** 导致 `XSS`攻击，低版本的`jq`和其他`npm`插件，容易有`Javascript`框架漏洞

解决方法：

- **`js-cookie` 引发的问题**

  `vue`项目中，引用了`js-cookie`来存储一些基础登录信息，容易导致`xss`攻击。

   用`localStorage`或`sessionStorage`来储存登录信息。

   

  ```js
  // 详细用法
  	const userInfo = JSON.srtingfy(userInfo)
  	// 储存数据
  	sessionStorage.setItem("userInfo",userInfo)
  	// 获取数据
  	let userInfo = JSON.parse(sessionStorage.getItem("userInfo"))
      // 删除数据
      sessionStorage.removeItem("userInfo")
  	// 清楚sessionStorage数据
      sessionStorage.clear()
  ```

- **`Jquery `系列解决问题**

  `JQ`只要升级至最新版本就可以解决

  

- **`vue`打包扫描出现高风险文件`YUI`版本太低问题 （`jsencrypt`）**

  全局搜索`YUI`，发现`vue`打包的文件里面含有这个版本名称，原来是`rsa`加密的插件`jsencrypt`导致

  ```js
  // 用npm 安装到项目安装得jsencrypt是**没有压缩**得，里面包含YUI打包之后会出现这种文件，
  // 所以 npm 安装了jsencrypt后 不要直接： import jsencryptf rom 'jsencrypt'，
  // 将node_module中的jsencrypt.min.js拿出，放到utils文件
  // 可在main.js引用
  import JSEncrypt from '../utils/jsencrypt.min.js'
  ```

- **高风险文件`YUI`版本太低问题 （`jsrsasign`）**

  解决办法： 改用 `jsencrypt`加密