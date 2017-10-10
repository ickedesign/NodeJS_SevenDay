# Day2_代码的组织和部署

## 包

### index.js

当模块的文件名是index.js，加载模块时可以使用模块所在目录的路径代替模块文件路径，因此接着上例，以下两条语句等价。

``` js
var cat = require('/home/user/lib/cat');
var cat = require('/home/user/lib/cat/index');
```

这样处理后，只需要把包目录路径传递给require函数，感觉上整个目录被当作单个模块使用，更有整体感。

### package.json

如果想自定义入口模块的文件名和存放位置，就需要在包目录下包含一个package.json文件，并在其中指定入口模块的路径。上例中的cat模块可以重构如下。

``` js
- /home/user/lib/
    - cat/
        + doc/
        - lib/
            head.js
            body.js
            main.js
        + tests/
        package.json
```

其中package.json内容如下：

``` js
{
    "name": "cat",
    "main": "./lib/main.js"
}
```

如此一来，就同样可以使用require('/home/user/lib/cat')的方式加载模块。NodeJS会根据包目录下的package.json找到入口模块所在位置。
