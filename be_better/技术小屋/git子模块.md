### **从零开始创建子模块的步骤：**

## 1. 在父仓库中初始化 Git 仓库
如果你还没有创建 Git 仓库，首先在父仓库目录下运行 `git init` 来初始化它：
`cd D:/code  # 进入父仓库目录 git init`
## 2. 创建或获取子模块仓库
假设你已经有了子模块仓库的 URL（例如 GitHub 上的仓库），如果没有，你可以先创建一个新的 Git 仓库，或者选择一个已经存在的仓库。假设子模块仓库的 URL 为：
`ssh://git@github.com/sorcerer-program/campus.git`
## 3. 将子模块添加到父仓库
使用 `git submodule add` 命令将子模块添加到父仓库。这会将子模块克隆到父仓库中的指定目录（例如 `python/campus`）。
`git submodule add ssh://git@github.com/sorcerer-program/campus.git python/campus`
- 这将：
    - 在父仓库中创建一个 `.gitmodules` 文件，记录子模块的信息。
    - 在 `python/campus` 目录下克隆子模块仓库的内容。
## 4. 初始化并更新子模块内容
运行 `git submodule init` 来初始化子模块，准备好使用 `.gitmodules` 文件中记录的配置。
`git submodule init`
然后，使用 `git submodule update` 拉取子模块的内容：
`git submodule update`
这会将子模块的内容从远程仓库下载到你的本地 `python/campus` 目录。
## 5. 提交父仓库的更改
现在，你已经成功地将子模块添加到父仓库，并且初始化并下载了子模块的内容。接下来，需要将 `.gitmodules` 文件和子模块的引用提交到父仓库。
`git add .gitmodules python/campus git commit -m "Add campus as a submodule" git push`
## 6. 操作子模块
如果你需要对子模块进行更改（例如切换分支或推送更改），你需要进入子模块的目录并进行操作：
`cd python/campus git checkout user/sorcerer  # 切换到特定的分支 `
`git push origin user/sorcerer  # 推送更改`
## 总结
1. **在父仓库中添加子模块**：  
    使用 `git submodule add <repo-url> <path>` 将子模块添加到父仓库。
2. **初始化和更新子模块**：  
    使用 `git submodule init` 和 `git submodule update` 初始化和拉取子模块的内容。
3. **提交更新到父仓库**：  
    提交 `.gitmodules` 文件和子模块的引用更新到父仓库。