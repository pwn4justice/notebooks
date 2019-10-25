## Mac Brew 源

```
替换brew.git:
cd "$(brew --repo)"
git remote set-url origin https://mirrors.ustc.edu.cn/brew.git

替换homebrew-core.git:
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git 
```



### 方法2

1. 获取 install 文件

```
curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install >> brew_install
```

2. 更改脚本中的资源链接

```
BREW_REPO = “https://github.com/Homebrew/brew“.freeze 
CORE_TAP_REPO = “https://github.com/Homebrew/homebrew-core“.freeze 
```

为

```
BREW_REPO = "https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git".freeze 
CORE_TAP_REPO = "https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git".freeze
```

3. 运行脚本

```
/usr/bin/ruby brew_install
```

注：添加清华大学镜像源：

```
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.tuna.tsinghua.edu.cn/homebrew-bottles'>>   ~/.bash_profile

source ~/.bash_profile
```

