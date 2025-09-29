# 字帖pdf的生成
## 完整的示例
```python
"""模块导入"""
from pdf import CalligraphyPdfHard, CalligraphyPdfSoft  
from web_to_local import paths_web_to_local
```
```python
"""字帖生成"""
hard_paths = [  
        'https://ygsf.cdn.bcebos.com/font/0/78743a5c2a5ae3be/0b210ed9aa1d9bf35fc9177969323efb.png?x-bce-process=style/png256&v=0',  
        'https://ygsf.cdn.bcebos.com/font/1/2a894f840216a020/bbdd0cc7ee2c9515f1522a867208cbab.png?x-bce-process=style/png256&v=0'  
]  

# 第一步：将网络图片下载到本地
hard_paths = paths_web_to_local(hard_paths, 1, save_dir='yingbi')  
# 第二步：生成字帖
hard_pdf = CalligraphyPdfHard(hard_paths, 1, 0, "output_hard.pdf")  
hard_pdf.generate_pdf()
```
## 参数说明
### 网络图片下载到本地传参说明
`paths_web_to_local(paths_web, tool, save_dir="temp", max_workers=4)`
"""  
    :param paths_web: 需要下载的图片网络路径（列表）  
    :param tool: 0-毛笔 1-硬笔  
    :param save_dir: 下载下来图片放入的文件夹  
    :param max_workers: 进程数（默认为4，可改）  
"""
### 生成字帖类的传参与以前一致
