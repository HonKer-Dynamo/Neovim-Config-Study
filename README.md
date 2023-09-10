# 环境变量

```text
XDG_CONFIG_HOME                D:\Study\Tools\Neovim\user_config
XDG_DATA_HOME                  D:\Study\Tools\Neovim\user_config
Path						   D:\Study\Tools\Neovim\bin
```

## 以上的三个环境变量在 PowerShell 中的 NeoVim 中具有以下作用：

##### 1.XDG_CONFIG_HOME: 该环境变量指定 NeoVim 的配置文件所在的路径。在你的情况下，它被设置为 D:\Study\Tools\Neovim\user_config。NeoVim 在启动时会使用该路径来寻找 init.vim（或者 init.lua）配置文件。通过设置该环境变量，你可以将配置文件放置在指定的路径，使其更加可管理和易于备份。

##### 2.XDG_DATA_HOME: 该环境变量指定 NeoVim 的数据文件所在的路径。在你的情况下，它同样被设置为 D:\Study\Tools\Neovim\user_config。NeoVim 在执行诸如插件安装、插件数据等操作时会使用该路径。通过设置该环境变量，你可以将数据文件存储在指定的路径，使其与配置文件分离，便于管理和维护。

##### 3.Path: 这是一个系统级环境变量，其中包含了一组用分号分隔的目录路径。将 NeoVim 的可执行文件路径 D:\Study\Tools\Neovim\bin 添加到 Path 环境变量中，可以使得在任何位置都可以直接运行 nvim 命令，而无需指定完整的路径。这样你就可以在 PowerShell 中直接运行 nvim 命令来启动 NeoVim。





# 安装插件管理工具vim-plug

https://www.cnblogs.com/joe-yang/p/17071125.html

### 例如我想安装的路径是：

```text
D:\Study\Tools\Neovim\user_config\nvim-data\site\autoload\plug.vim
```

### 打开powershell后使用下面的代码即可下载

#### 环境变量版

```Windows (PowerShell)
iwr -useb https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim |`
    ni "$(@($env:XDG_DATA_HOME, $env:LOCALAPPDATA)[$null -eq $env:XDG_DATA_HOME])/nvim-data/site/autoload/plug.vim" -Force
```

#### 绝对路径版

```powershell
iwr -useb https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim | ni "D:\Study\Tools\Neovim\user_config\nvim-data\site\autoload\plug.vim" -Force

```





## 为vim-plug编写init.vim文件来下载并且自动更新

### 环境变量版：

```init.vim
" 安装vim-plug插件管理器
if empty(glob('$XDG_DATA_HOME\nvim-data\site\autoload\plug.vim'))
  silent !curl -fLo $XDG_DATA_HOME\nvim-data\site\autoload\plug.vim --create-dirs
        \ https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
  autocmd VimEnter * PlugInstall --sync | source $MYVIMRC
endif

" 插件配置和安装列表
call plug#begin('$XDG_DATA_HOME\nvim-data\plugged')

" 在这里添加你要安装的插件

call plug#end()

" 自动更新插件
filetype plugin indent on

```

### 绝对路径版

```init.vim
" 安装vim-plug插件管理器
if empty(glob('D:\Study\Tools\Neovim\user_config\nvim-data\site\autoload\plug.vim'))
  silent !curl -fLo D:\Study\Tools\Neovim\user_config\nvim-data\site\autoload\plug.vim --create-dirs
        \ https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
  autocmd VimEnter * PlugInstall --sync | source $MYVIMRC
endif

" 插件配置和安装列表
call plug#begin('D:\Study\Tools\Neovim\user_config\nvim-data\plugged')

" 在这里添加你要安装的插件

call plug#end()

" 自动更新插件
filetype plugin indent on


```

## 测试：输入插件安装命令会提示

### 命令：

```vim
:PlugInstall
```

### 提示：

```vim
No Plugin to install
```





# 安装packer.nvim

### Windows Powershell 默认安装命令

```powershell
git clone https://github.com/wbthomason/packer.nvim "$env:LOCALAPPDATA\nvim-data\site\pack\packer\start\packer.nvim"
```

### 输出：

```powershell
Cloning into 'C:\Users\HonKe\AppData\Local\nvim-data\site\pack\packer\start\packer.nvim'...
remote: Enumerating objects: 4737, done.
remote: Counting objects: 100% (1240/1240), done.
remote: Compressing objects: 100% (388/388), done.
remote: Total 4737 (delta 916), reused 1064 (delta 845), pack-reused 3497
Receiving objects: 100% (4737/4737), 1.37 MiB | 2.38 MiB/s, done.
Resolving deltas: 100% (2694/2694), done.
```

### Windows Powershell 环境变量版安装命令

```powershell
git clone https://github.com/wbthomason/packer.nvim "$env:XDG_DATA_HOME\nvim-data\site\pack\packer\start\packer.nvim"
```

### 输出：

```powershell
Cloning into 'D:\Study\Tools\Neovim\user_config\nvim-data\site\pack\packer\start\packer.nvim'...
remote: Enumerating objects: 4737, done.
remote: Counting objects: 100% (1268/1268), done.
remote: Compressing objects: 100% (399/399), done.
remote: Total 4737 (delta 939), reused 1082 (delta 862), pack-reused 3469
Receiving objects: 100% (4737/4737), 1.37 MiB | 4.65 MiB/s, done.
Resolving deltas: 100% (2694/2694), done.
```



### Windows Powershell 绝对路径版安装命令

```powershell
git clone https://github.com/wbthomason/packer.nvim "D:\Study\Tools\Neovim\user_config\nvim-data\site\pack\packer\start\packer.nvim"
```

### 输出：

```powershell
Cloning into 'D:\Study\Tools\Neovim\user_config\nvim-data\site\pack\packer\start\packer.nvim'...
remote: Enumerating objects: 4737, done.
remote: Counting objects: 100% (1240/1240), done.
remote: Compressing objects: 100% (388/388), done.
remote: Total 4737 (delta 916), reused 1064 (delta 845), pack-reused 3497
Receiving objects: 100% (4737/4737), 1.37 MiB | 14.77 MiB/s, done.
Resolving deltas: 100% (2694/2694), done.
```





# 为packer.nvim配置init.lua文件

### 环境变量版

```init.lua
-- 设置 packer.nvim 的安装路径
vim.cmd(string.format('packadd packer.nvim'))
local install_path = vim.fn.stdpath('data') .. '/site/pack/packer/start/packer.nvim'
if vim.fn.empty(vim.fn.glob(install_path)) > 0 then
    vim.fn.system({'git', 'clone', 'https://github.com/wbthomason/packer.nvim', install_path})
    vim.cmd('packadd packer.nvim')
end

-- 初始化 packer.nvim
return require('packer').startup(function()
    -- 在这里添加你要安装的插件
    use {'your_plugin_name/repository'}
end)

```

### 绝对路径版

##### 在 Windows 系统中，路径分隔符通常是反斜杠 `\`。但是，在 Lua 代码中，反斜杠 `\` 是转义字符，用于表示特殊字符（例如换行符 `\n` 或制表符 `\t`）。因此，如果你想在 Lua 配置文件中表示一个反斜杠，你需要使用两个反斜杠 `\\`。

```init.lua
-- 设置 packer.nvim 的安装路径
vim.cmd(string.format('packadd packer.nvim'))
local install_path = 'D:\\Study\\Tools\\Neovim\\user_config\\nvim-data\\site\\pack\\packer\\start\\packer.nvim'
if vim.fn.empty(vim.fn.glob(install_path)) > 0 then
    vim.fn.system({'git', 'clone', 'https://github.com/wbthomason/packer.nvim', install_path})
    vim.cmd('packadd packer.nvim')
end

-- 初始化 packer.nvim
return require('packer').startup(function()
    -- 在这里添加你要安装的插件
    use {'your_plugin_name/repository'}
end)

```

### 命令

```vim
:PackerCompile： 每次改变插件配置时，必须运行此命令或 PackerSync, 重新生成编译的加载文件
:PackerClean ： 清除所有不用的插件
:PackerInstall ： 清除，然后安装缺失的插件
:PackerUpdate ： 清除，然后更新并安装插件
:PackerSync : 执行 PackerUpdate 后，再执行 PackerCompile
:PackerLoad : 立刻加载 opt 插件
```



### 测试

```vim
:PackerStatus
```

#### 会显示packer和packer.nvim - Total plugins: 0的窗口

#### PackerStatus命令的作业是





# 关于Neovim init配置文件冲突的问题

##### 示例报错：

```nvim
E5422: Conflicting configs: "D:\Study\Tools\Neovim\user_config\nvim\init.lua" "D:\Study\Tools\Neovim\user_config\nvim\init.vim"
```

# 方法一（推荐）

#### 使用lua来分别管理插件和设置等等

```text
路径：D:\Study\Tools\Neovim\user_config\nvim\lua
文件：
basic.lua
keybindings.lua
plugins.lua
vim-plug.lua
```





### 保留init.vim示例

```init.vim
" 自定义配置

" 基础设置
execute 'luafile ' .. expand('$XDG_DATA_HOME/nvim/lua/basic.lua')

" 快捷键映射
execute 'luafile ' .. expand('$XDG_DATA_HOME/nvim/lua/keybindings.lua')

" Packer 插件管理
execute 'luafile ' .. expand('$XDG_DATA_HOME/nvim/lua/plugins.lua')

" vim-plug 插件管理
execute 'luafile ' .. expand('$XDG_DATA_HOME/nvim/lua/vim-plug.lua')

```

### 保留init.lua示例

```init.lua
--自定义配置
-- 基础设置
require('basic')
-- 快捷键映射
require("keybindings")
-- Packer 插件管理
require("plugins")
-- vim-plug 插件管理
require("vim-plug")
```

### 方法二：

### 保留init.vim文件

```text
如果你想保留 `init.vim` 文件并删除 `init.lua` 文件，你可以按照以下步骤操作：

1. 打开 `init.lua` 文件并将其内容复制。
2. 打开 `init.vim` 文件并将复制的内容粘贴到文件末尾。
3. 保存 `init.vim` 文件并关闭文本编辑器。
4. 删除 `init.lua` 文件。

这样，你就可以保留 `init.vim` 文件并删除 `init.lua` 文件，同时保留两个文件中的所有配置。
```

### 保留init.lua文件

```text
如果你想保留 `init.lua` 文件并删除 `init.vim` 文件，你可以按照以下步骤操作：

1. 打开 `init.vim` 文件并将其内容复制。
2. 打开 `init.lua` 文件并将复制的内容粘贴到文件末尾。
3. 保存 `init.lua` 文件并关闭文本编辑器。
4. 删除 `init.vim` 文件。

这样，你就可以保留 `init.lua` 文件并删除 `init.vim` 文件，同时保留两个文件中的所有配置。
```



