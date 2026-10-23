# 网站源码更新

`site-source/` 保存已经修改的源码文件，目录结构与原项目相同，并不是完整源码副本。发布时，GitHub Actions 先将仓库内的 `zhixue-atlas-source.zip` 解压到临时构建目录，再用此目录中的文件覆盖同名文件。原有图片和未修改的源码继续来自 ZIP。

后续优化无需手动重新上传 ZIP。在 GitHub 网页打开 `site-source/` 内的文件，使用编辑按钮修改并提交到 `main`；新增文件也应放在与原项目一致的相对路径。例如，修改页面可提交为 `site-source/app/page.tsx`。提交后会自动检查、构建并发布网站，发布状态可在仓库的 Actions 页面查看。

此目录是文件覆盖层：删除其中的文件会恢复 ZIP 中的原版，不代表删除原项目文件。需要删除原有文件或进行较大的目录调整时，应同步调整构建方式，或迁移为完整源码仓库。

新增或升级依赖时，必须一起更新 `site-source/package.json` 和 `site-source/package-lock.json`，确保 `npm ci` 能按锁定版本安装。

`public/deployment-channel.json` 用于验证源码文件已被发布。每次构建还会生成公开的 `deployment.json`，其中仅包含提交编号、运行编号和仓库名，可用于核对线上版本。这些文件不改变网站界面。

GitHub Pages 承载静态网页。当前 AI 讲解、图片识别和自动课程搜索等 API 功能仍需要独立部署后端，并在网站设置中填写后端服务地址；本次发布流程不会自动部署该后端。
