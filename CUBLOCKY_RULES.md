# CuBlocky 网站部署规则

## 背景
- GitHub Pages 是纯静态托管，没有任何后端
- CuBlocky 本体有后端 API（编译、保存项目、资源管理等），不能直接用
- 每次部署必须从远程拉最新源码，在副本上改好再构建，绝不能动原版

## 部署流程
1. 从 https://github.com/mouse114514/CuBlocky 的 master 分支下载源码（zip）
2. 解压到临时目录
3. 修改源码适配纯静态环境
4. `npx vite build`（跳过 tsc，因为可能有类型错误）
5. 复制 `server/wwwroot/` 的构建产物（assets、media、favicon）到 ouse-site 根目录
6. 更新 index.html 的 JS/CSS 文件名
7. 推送 ouse-site

## 必须做的修改（适配纯静态）

### 1. 欢迎页
- 去掉「新建项目」「打开项目」两个按钮（都需要后端 API）
- 改成一个「开始」按钮，点击直接进入编辑器
- 保留语言切换（中/英/俄）
- 保留底部 Nexus Mods / GitHub 链接

### 2. 工具栏
- 砍掉「构建 DLL」按钮及相关逻辑
- 砍掉「资源管理」按钮及相关逻辑（AssetManager 组件不需要）
- 保留「另存为」→ 改为下载 .cbp 文件到本地（用 Blob + download）
- 保留「打开」→ 用文件选择器打开本地 .cbp 文件（用 `<input type="file">`）
- 保留代码预览切换

### 3. 其他
- 所有 `/media/` 路径保持绝对路径（从根目录提供服务）
- favicon 和 media 文件必须一起部署
- 不要删除 `function.png` 等新增图标

## 已废弃/不部署
- GlassX（已废弃）
- CCL-Checker（不是 Mod，不上网站）
