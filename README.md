## learn luarocks

- https://github.com/keplerproject/luarocks/wiki/Creating-a-rock
- https://github.com/keplerproject/luarocks/wiki/write_rockspec
- https://segmentfault.com/a/1190000003920034

## step by step

- 去luarocks.org 注册帐号，并生成api- key
- 去github上生成一个空项目
- source code 部分
  - git clone https://github.com/zqWu/luarocks_helloworld
  - 生成 rockspec 文件
    ```
    luarocks write_rockspec luarocks_helloworld 1.0.0 ./
    ```

  - 编辑 `luarocks_helloworld-1.0-1.rockspec`

    ```
    package = "luarocks_helloworld"
    version = "1.0-1"
    source = {
      url = "https://github.com/zqWu/luarocks_helloworld",
      tag = "v1.0"
    }
    description = {
      license = "MIT"
    }
    dependencies = {}
    build = {
      type = "builtin",
      modules = {
        apple = "src/apple.lua"
      }
    }
    ```

  - src/apple.lua

    ```
    local  print = print

    local _M = {}
    setfenv (1, _M)

    function _M.info ()
      print("apple")
    end

    return _M
    ```

  - 文件结构
    ```
    .
    ├── LICENSE
    ├── luarocks_helloworld-1.0-1.rockspec
    ├── README.md
    └── src
        └── apple.lua
    ```

- tag v1.0 and push，
  ```
  git add -A && git commit -m "bla"
  git tag -a "v1.0" -m "v1.0"
  ```

> 如果没有tag，会有问题，官网上也推荐这种方法

- 发布

  ```
  luarocks pack luarocks_helloworld-1.0-1.rockspec
  luarocks upload --api-key=<your-key> luarocks_helloworld-1.0-1.rockspec
  ```


- 检测 https://luarocks.org/modules/dormi330/
  - 安装  `sudo luarocks install luarocks_helloworld`
  - ls /usr/local/lib/luarocks/rocks/luarocks_helloworld/
  - ls /usr/local/share/lua/5.1/apple.lua

  ```
  > lua
  > apple = require('apple')
  > apple.info()
  ```
