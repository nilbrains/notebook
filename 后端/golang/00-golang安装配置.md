# Golang安装配置

[Get Started - The Go Programming Language (google.cn)](https://golang.google.cn/learn/)

### 1. 去官网或者镜像站下载软件包

略

### 2. 进行安装

选择安装路径或者默认

下一步即可

在命令行

```bash
# 输入
go version
# 输出
go version go1.17.7 windows/amd64
```

出现版本号 安装成功

### 3. 修改环境变量

查看环境变量

```bash
# 输入
go env

# 输出
set GO111MODULE=
set GOARCH=amd64
set GOBIN=
set GOCACHE=C:\Users\nilbr\AppData\Local\go-build
set GOENV=C:\Users\nilbr\AppData\Roaming\go\env
set GOEXE=.exe
set GOEXPERIMENT=
set GOFLAGS=
set GOHOSTARCH=amd64
set GOHOSTOS=windows
set GOINSECURE=
set GOMODCACHE=C:\Users\nilbr\go\pkg\mod
set GONOPROXY=
set GONOSUMDB=
set GOOS=windows
set GOPATH=C:\Users\nilbr\go
set GOPRIVATE=
set GOPROXY=https://proxy.golang.org,direct
set GOROOT=D:\Develop\Go
set GOSUMDB=sum.golang.org
set GOTMPDIR=
set GOTOOLDIR=D:\Develop\Go\pkg\tool\windows_amd64
set GOVCS=
set GOVERSION=go1.17.7
set GCCGO=gccgo
set AR=ar
set CC=gcc
set CXX=g++
set CGO_ENABLED=1
set GOMOD=NUL
set CGO_CFLAGS=-g -O2
set CGO_CPPFLAGS=
set CGO_CXXFLAGS=-g -O2
set CGO_FFLAGS=-g -O2
set CGO_LDFLAGS=-g -O2
set PKG_CONFIG=pkg-config
set GOGCCFLAGS=-m64 -mthreads -fno-caret-diagnostics -Qunused-arguments -fmessage-length=0 -fdebug-prefix-map=C:\Users\nilbr\AppData\Local\Temp\go-build3019328905=/tmp/go-build -gno-record-gcc-switches
```

我们只需重点关注GOROOT、GOPATH、GOPROXY即可

**GOPROXY** 代理

```bash
 go env -w GOPROXY=https://mirrors.aliyun.com/goproxy/
```

修改代理 走 阿里云

**GO111MODULE** 是否开启 模块

```bash
go env -w GO111MODULE=on
```