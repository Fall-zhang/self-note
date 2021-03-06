> Create by **fall** on ——
> Recently revised in 2022-05-13

## npm 命令的使用

npm 的功能：

- 允许用户从 NPM 服务器下载别人编写的**第三方包**到本地使用。
- 允许用户从 NPM 服务器下载并安装别人编写的**命令行程序**到本地使用。
- 允许用户将自己编写的包或命令行程序上传到 NPM 服务器供别人使用。

### npm 下载

npm 在 Node V10 之后就自带了，不需要额外下载。

LTS 版本:  Long Term Support（[长期支持版本](https://nodejs.org/en/about/releases/)）

- 官方网址：https://nodejs.org
- 安装 npm 组件：https://www.npmjs.com

> 注：因为某些大家知道的原因，需要更换为国内的镜像，或者安装 yarn，代替 npm
>
> 当然，你可以通过该命令 `npm config get registry` 查看当前使用的镜像。默认：`https://registry.npmjs.org/`
>
> 可以使用 `npm config set registry https://registry.npm.taobao.org` 更改使用的镜像地址，当然也可以使用这个方法改回原来的地址。
>
> 安装 cnpm：`npm install -g cnpm --registry=https://registry.npm.taobao.org`
>
> 安装完成之后就可以通过 cnpm 代替 npm 的所有命令（有些插件使用 cnpm 安装，可能会出现问题）
>
> `npm -v` 用于检测 npm 是否安装成功

### 版本控制

**语义化版本控制**：简单来讲所有版本都有三个数字

- 第一个数字是主板本，进行不兼容的 API 更改时，升级主板本。
- 第二个数字是次版本，进行不兼容的 API 更改时，升级主板本。
- 第三个数字是补丁版本，向后兼容的缺陷修复时，升级补丁版本

### npm 命令

**npm 包的安装命令**

- 本地的安装包：使用`npm install <package-name>` 安装，并且放置在 node_modules 文件夹中
- 全局的安装包：`npm install <package-name> -g` 全局安装，并放在固定的位置。

> **通常所有软件包都应该本地安装**，可以确保计算机中有数十个应用程序，如果需要，每个应用都可以运行不同的版本。更新全局安装包时，所有的项目都使用新的版本，可能导致维护上的噩梦，可能会破坏原来的依赖项和兼容性等。

**安装命令详解**

```bash
# 示例：
npm install gulp@3.9.1 --save-dev  
# 功能：使用 npm 安装 gulp 的3.9.1版本版本
--save  # 表示安装在当前文件夹下，npm 5 之后的版本可以省略，也可以整体简写为 -S
-dev    # 将安装的信息保存在 package.json 中，作为开发依赖添加到 devDependencies 列表，简写为：-D
--save-dev # 多个命令串联
gulp@3.9.1 # 表示下载 3.9.1 版本的 gulp
npm install gulp@3.9.1 --save-dev # 的简写:npm i gulp@3.9.1 -S-D
```

**卸载命令**

`npm uninstall <package-name>`  卸载 node.js 指定的包

`npm uninstall <package-name> -g` 安装全局模块 -g 后进行全局模块的卸载

如果安装时使用 -S(即--save) ，卸载时必须添加 -S ，移除在 package.json 中的引用

同理，使用-D(--save-dev)，卸载时必须添加 -D

**其他命令**

线上查找模块 `npm search react`

| 命令（常用命令）                   | 功能                                                         |
| ---------------------------------- | ------------------------------------------------------------ |
| `npm list`                         | 列出当前工作区已经安装模块                                   |
| `npm list -g`                      | 查看全局安装的所有模块，只查找主要模块<br />`npm list -g --depth=0` |
| `npm root -g`                      | 查看全局模块的安装路径<br />如果使用 nvm 管理工具，位置可能会不同 |
| `npm init`                         | 创建 JSON 文件，初始化本地开发环境                           |
| `npm update`                       | 升级当前目录下的项目的所有模块                               |
| `npm search <key-word>`            | 按照关键字，在网络上搜索模块                                 |
| `npm view <package-name>`          | 在网络中查看该插件的详情                                     |
| `npm view <package-name> version`  | 查看该软件的最新版本                                         |
| `npm view <package-name> versions` | 查看该插件的所有版本                                         |
| `npm publish`                      | 发布模块                                                     |
| `npm config get cache`             | 查看 缓存所在位置                                            |



## NPX工具

npx 是一个工具，可以自动寻找当前文件夹（node_modules）文件夹下的可执行插件，正确引用并且执行。并且如果当前文件夹下没有下载可执行插件，那就会在网络中寻找后，下载并且运行，在运行成功后删除，利用这一特性，可以实现避免全局模块的安装。

> 命令的使用类似于原插件的执行方法，不过不需要 npm 进行安装：
>
> `npx cowsay hello world`
>
> 可以和 node 特定版本结合，`npx node@10 -v #10.18.1`

```bash
npx uglify-js@3.1.0 // 同 npm 一样，可以通过@指定使用的版本
```

**可添加的参数**

`--no-install` 强制使用本地模块

`--ignore-existing` 忽略本地存在的模块

```bash
 npx --no-install http-server // 强制使用本地模块
 npx --ignore-existing create-react-app my-react-app // 忽略本地存在的模块，然后生成react app
```

`-p` 指定将要安装的模块

```bash
npx -p node@0.12.8 node -v 
npx -p lolcatjs -p cowsay "hello" // 可以通过 -p 指定多个不同的命令
```

`-c` 可以将所有命令都用 npx 解释，

```bash
npx -p lolcatjs -p cowsay 'cowsay hello | lolcatjs' // 报错
// 默认情况只有第一个可执行项会使用 npx 安装的模块，后面的可执行项还是会交给 Shell 解释。
npx -p lolcatjs -p cowsay -c 'cowsay hello | lolcatjs' // 添加 -c 后将所有命令给 npx 解释，正常运行
```

将环境变量带入所要执行的命令

```bash
npm run env | grep npm_ // 可以用该命令查看提供当前项目的一些环境变量。
npx -c 'echo "$npm_package_name"' // 该代码会输出当前项目的项目名
```

### 执行远程代码

npx 可以指定直接执行 git 上面的代码，前提是远程代码必须是一个模块，必须包含 package.json 和入口脚本。

用 npx 使用 live-server

使用 `npx http-server`

> yarn & pnpm
>
> yarn 和 pnpm 都是为了解决 npm 上出现的一些固有的错误，而进行开发的。pmpm 的[官方文档](https://pnpm.io/zh/pnpm-cli)
>
> 现在 PNPM 也作为包管理工具进行使用

## NVM命令的使用

### 什么是NVM

nvm是用来**对 node 进行版本控制的工具**

> 注：windows 上运行的 nvm 和 linux & MacOS 上的 nvm 工具不是一个项目，它们是两个团队做出来的东西。

nvm（Linux、Unix、OS X）的安装：https://github.com/creationix/nvm

nvm（Windows）安装：https://github.com/coreybutler/nvm-windows

### 常用命令

基本命令

```bash
# 安装最新版本的 node
nvm install node 
nvm install latest
# 当前所拥有的 node 的版本
nvm list
nvm ls
# 切换到淘宝镜像
nvm use taobao
# 全局安装 nvm 命令（使用 cnpm 安装 nvm）
cnpm install -g nvm
# 当前nvm工具的版本
nvm -v
# 使用 8.4.0 版本的 node
nvm use 8.4.0 
# 卸载该版本的 node.js
nvm uninstall 8.4.0
```
