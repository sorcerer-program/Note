
在原有的基础上，添加对图片网址的处理，如果传入的url是网址而非本地路径，则在创建类之前调用`paths_web_to_local()`对paths进行处理
```python
	def paths_web_to_local(paths_web):  
	"""
	:param paths_web: 传入的网址（复数）
	:return: 本地图片地址（复数）
	"""
```
举例
```python
soft_paths = [  
    "https://ygsf.cdn.bcebos.com/autogen/areas/80db6894e7860be78f40cf7b59226581/26/f02487e94c2d00f9a07832087ababd22_.png?x-bce-process=style/jpg256",  
    "https://ygsf.cdn.bcebos.com/autogen/areas/cd54af3757f36050d3aec9aad2d1707e/10/567d485299cd885e5f3069cdc3f42c58_.png?x-bce-process=style/jpg256"  
]  
soft_paths = paths_web_to_local(soft_paths)
```

## 毛笔
### 类的说明
`CalligraphyPdfSoft(img_paths, individuation, size, output_path)`
```python
:img_paths: 多个要生成字的原始图片，列表传入
:individuation: 个行化定制 0：一页一字  1：一行一字  2：一行多字
:size: 要生成的毛笔字大小 0：超小  1：小号  2：中号  3：大号
:output_path: 生成的pdf路径
```
### 应用举例：

#### 将网址改为本地地址
`soft_paths = paths_web_to_local(soft_paths)`
#### 创建类
`var = CalligraphyPdfSoft(soft_paths, 0, 0, "超小毛笔一页一字.pdf")`
#### 生成pdf
`var.generate_pdf()`

## 硬笔
### 类的说明
`CalligraphyPdfHard(img_paths, individuation, method, output_path)`
```python
:img_paths: 多个要生成字的原始图片，列表传入
:individuation: 个行化定制 0：一页一字  1：一行一字  2：一行多字
:method: 使用字帖的方式  0：描红  1：跟写
:output_path: 生成的pdf路径
```
### 应用举例：
#### 将网址改为本地地址
`soft_paths = paths_web_to_local(soft_paths)`
#### 创建类
`var = CalligraphyPdfHard(hard_paths, 0, 0, "描红硬笔一页一字.pdf")`
#### 生成pdf
`var.generate_pdf()`
