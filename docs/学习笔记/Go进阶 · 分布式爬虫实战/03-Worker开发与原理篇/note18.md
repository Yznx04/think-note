# 18-依赖管理：Go Module的用法和原理

Go中的依赖管理经过了漫长的演进过程。在Go1.5之前采用GOPATH进行管理，中间出现过vendor, 最终演进为Go1.11版本后的Go Modules。

## GOPATH

在Go1.8版本以上，如果不指定GOPATH，GOPATH的路径是默认的，可以使用命令`go env GOPATH`查看。在Linux和Mac操作系统中，在`$HOME/go`，
Windows中是`%USERPROFILE%\go`。GOPATH可以理解为Go的工作空间，内部存储了src、bin、pkg三个文件夹：

- bin：存储了go install安装的二进制文件。
- pkg：不同操作系统有不同的文件夹，存储预编译的obj文件，以加快程序的后续编译。mod文件会存储Go Modules的依赖。
- src：存储项目的Go代码。

## Go Modules

Go1.13版本后，目录下只要有go.mod文件，Go编译器默认通过Go Modules来管理依赖。

Go Modules支持模块名称与导入路径不一致：

```
a github.com/b/c
```

## Go Module实战

初始化：

```
go mod init github.com/yznx/moduleName
```

同步依赖

```
go mod tidy
```

