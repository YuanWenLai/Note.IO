# npm运行错误集

## npm install 运行报错



### 1.npm intsall 运行报错，错误代码128

#### 报错信息：

```
error Error while executing:
error D:\Git\Git\bin\git.EXE ls-remote -h -t git://github.com/adobe-webplatform/eve.git
error
error fatal: unable to look up github.com (port 9418) (Ӧ�ó���û�е��� WSAStartup������ WSAStartup ʧ�ܡ� )
error
error exited with error code: 128
verbose exit [ 1, true ]
```

#### 解决方案：

+ 方法一

  ```
  git config --global http.sslverify "false"
  npm install
  ```

+ 方法二：

  方法二比方法一有效

  ```
  git config --global url."https://".insteadof git://
  ```



### 2.npm install 出现"Unexpected end of JSON input while parsing near..."

#### 解决方案：

+ 方法一：

  ```
  npm cache clean --force
  ```



### 3.Module build failed : TypeError:this.getResolve is not a function at Object.loader 安装sass-loader版本错误

#### 解决方案：

+ 方法一：

  ```
  //原因：sass的8.0.0版本过高，webpack编译错误，降低sass-loader的版本即可
  npm uninstall sass-loder
  npm insatll -s sass-loader@7.3.1
  ```



### 4.Error:EBUSY:resource busy or loacked,symlink

#### 解决方案：

+ 方法一：

  ```
  //原因：当npm install安装依赖包时，出现报错
  //关掉电脑杀毒软件，比如360等等
  ```



### 5.npm ERR! code ELIFECYCLE

#### 解决方案：

+ 方法一：

  ```
  //1.先删除node_modules
  //2.npm install rimraf -g
  //3.然后rimraf node_modules
  //4.最后npm install
  ```



### 6. npmERR!Windows_NT 6.1.7601

#### 解决方案：

+ 方法一：

  ```
  //1.关闭npm的https： npm sonfig set strict-ssl false
  //清理npm的代理命令：npm config delete http-proxy,npm config delete https-proxy
  //设置npm的获取地址：npm config set registry "http://registry.npmjs.org"
  ```

+ 方法二：

  ```
  //1.设置npm获取的代理服务器地址
  npm install -g cnpm --registry=http://r.cnpmjs.org
  npm install microtime --registry=http://r.cnpmjs.org --disturl=http://dist.cnpmjs.org

  ```

