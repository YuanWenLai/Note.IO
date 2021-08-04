## `webpack`的source map

### 1、什么是source  map？

它是一个独立的map文件，与源码在同一个目录下，可以通过 source map 定位到源代码

1. source map科普⽂： http://www.ruanyifeng.com/blog/2013/01/javascript_source_map.html
2. source map是开发环境时开启，线上环境关闭。但可以线上排查问题的时候，将source map的错误日志上传到系统



### 2、source  map的关键字

- eval： 使用eval包裹的模块代码
- source  map：产生.map文件
- cheap：不包含列信息
- inline：将.map作为DataUrl嵌入，不单独生成.map文件
- module：包含loader的source map



### 3、source  map类型

+ +-代表构建速度

| devetool                       | 首次构建 | 二次构建 | 适合生产环境 | 可以定位的代码                     |
| ------------------------------ | -------- | -------- | ------------ | ---------------------------------- |
| none                           | +++      | +++      | yes          | 最终输入的代码                     |
| eval                           | +++      | +++      | no           | webpack生成的代码（模块）          |
| cheap-eval-source-map          | +        | ++       | no           | 经过loader转换后的代码（只能看行） |
| cheap-module-eval-source-map   | O        | ++       | no           | 源代码（只能看行）                 |
| eval-source-map                | --       | ++       | no           | 源代码                             |
| cheap-source-map               | +        | O        | yes          | 经过loader转换后的代码（只能看行） |
| cheap-module-source-map        | O        | -        | yes          | 源代码（只能看行）                 |
| inline-cheap-source-map        | +        | O        | no           | 经过loader转换后的代码（只能看行） |
| inline-cheap-module-source-map | O        | -        | no           | 源代码（只能看行）                 |
| source-map                     | --       | --       | yes          | 源代码                             |
| inline-source-map              | --       | --       | no           | 源代码                             |
| hidden-source-map              | --       | --       | yes          | 源代码                             |

