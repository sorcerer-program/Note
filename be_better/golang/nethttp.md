---
date: 2025-10-13
tags:
  - golang
  - net
  - http
---
## Handler & HandlerFunc & HandleFunc
### Handler
Handler 是接口，任何实现了`ServeHTTP(w,r)`方法的类型都是 Handler 。
```go
type Handler interface {
    ServeHTTP(ResponseWriter, *Request)
}
```
主要用途
```go
http.Handle(pattern string, handler Handler)
```
示例
```go
type MyHandler struct {}

func (h MyHandler) ServeHTTP(w http.ResponseWriter, r *http.Request) {
	// 处理的逻辑
}

// 注册路由
http.Handle("/path", MyHandler{})
```
### HandlerFunc
HandlerFunc 是一个函数类型，将处理逻辑的函数转化为Handler的函数，它Handler对应实现的ServeHTTP函数就是处理逻辑的函数。
```go
type HandlerFunc func(ResponseWriter, *Request)

func (f HandlerFunc) ServeHTTP(w ResponseWriter, r *Request) {
	f(w, r)
}
```
示例
```go
// 某处理问题的逻辑函数
func deal(w http.ResponseWriter, r *http.Request) {
	// 具体的逻辑
}

// 将deal包装成HandlerFunc  类型转换
http.Handle("/deal", http.HandlerFunc(deal))
```
### HandleFunc
本质上是方便写。写的时候直接写（路由， 解决的函数）
```go
func HandleFunc(pattern string, handler func(ResponseWriter, *Request)) {
	http.Handle(pattern, http.HandlerFunc(handler))
}
```
