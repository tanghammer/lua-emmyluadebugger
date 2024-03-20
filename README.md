# lua-emmyluadebugger
A OpenWrt package of EmmyLuaDebugger

- [IntelliJ-EmmyLua](https://github.com/EmmyLua/IntelliJ-EmmyLua)
- [EmmyLuaDebugger](https://github.com/CppCXY/EmmyLuaDebugger)

[IntelliJ-EmmyLua](https://github.com/EmmyLua/IntelliJ-EmmyLua)是一个给JetBrains全家桶用的lua插件，也有VSCode版本[VSCode-EmmyLua](https://github.com/EmmyLua/VSCode-EmmyLua)插件。

[EmmyLuaDebugger](https://github.com/CppCXY/EmmyLuaDebugger)是配合IntelliJ-EmmyLua使用的remote debugger, C++编写供lua调用的动态库（emmy_core.so），相比于我以前使用的mobdebug具有更高的性能。

[lua-emmyluadebugger](https://github.com/tanghammer/lua-emmyluadebugger)是EmmyLuaDebugger的OpenWrt包，host cmake最低版本需要3.15(使用openwrt v19.07的即可),不然要修改EmmyLuaDebugger的CMakeLists.txt。

- ### 使用方法（基于clion）

  - 安装Emmylua插件

  - 使用clion的deployment将openwrt根文件系统拉到开发机器上（openwrt的根文件系统编译好tftp，手动rsync也行）
  - clion添加一个配置：Run >> Edit Configuration >> + ,选择Emmy Debugger，然后配置参数，IDE这端作为Server所以connection选择Debugger connect IDE，配好本机ip和监听端口。
  - 拷贝clion上自动生成的lua代码到lua的入口文件/www/cgi-bin/luci的第一行
  ```lua
  -- openwrt上这句可以不要
  -- package.cpath = package.cpath .. ';/home/a/.local/share/JetBrains/CLion2023.3/EmmyLua/debugger/emmy/linux/?.so'
  local dbg = require('emmy_core')
  dbg.tcpConnect('192.168.3.3', 9966)
  ```
  - 下一个断点，进入luci的web，好了，debugg吧！
