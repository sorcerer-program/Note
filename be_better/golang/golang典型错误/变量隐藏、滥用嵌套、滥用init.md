---
date: 2025-09-18
tags:
  - 典型错误
  - 变量隐藏
  - 嵌套
  - init
  - golang
---
## 1. 变量隐藏
某个作用域里面重新定义了一个与外层同名变量，外层同名变量杯隐藏。
```go
var client *http.Client
if tracing {
	client, err := creatClientWithTracing()
} else {
	client, err := creatDefaultClient()
}
// 接下来对client进行操作
```
` := `是临时变量，接下来对` client `的操作会出问题，因为` client `还是` nil `。可以加一个临时变量，然后把临时变量赋给` client `。
## 2. 滥用嵌套
` if-else `屎山很难读，特别是` else `里面又套` if `。实在避免不了就不用` else `，好读一些。
## 3. 滥用init
### init执行顺序
` init `在初始化时执行，所有的` init `在` main() `之前被调用。
1. 同包，执行顺序由源文件字母顺序确定。
2. 异包，包间初始化顺序依赖导入关系。
### init易错点
* 限制错误管理，不返回错误，直接` panic `退出。
* 如果初始化需要设置一个状态，只能用全局变量，单元测试更加复杂，任何函数都可修改全局变量不安全。


