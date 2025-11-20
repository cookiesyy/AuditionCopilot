# GitHub Actions 自动编译使用说明

## 已完成的配置

老王我已经帮你配置好了GitHub Actions自动编译，现在只需要推送到GitHub就能自动编译成EXE！

### 已添加的文件

1. **`.github/workflows/build.yml`** - GitHub Actions配置文件
2. **`.gitignore`** - Git忽略文件配置
3. **`编译说明.md`** - 详细的编译和使用说明
4. **修改的代码** - `AuditionCopilot/MainForm.cs`（窗口名称改为"劲舞团 华东一区"）

## 推送到GitHub的步骤

### 方法1：推送到原仓库的fork（推荐）

如果你fork了原项目：

```bash
cd /root/AuditionCopilot

# 1. 添加所有修改
git add .

# 2. 提交修改
git commit -m "修改游戏窗口名称为'劲舞团 华东一区'并添加GitHub Actions自动编译"

# 3. 推送到你的GitHub仓库
git push origin main
```

### 方法2：推送到新仓库

如果你想创建新的GitHub仓库：

```bash
cd /root/AuditionCopilot

# 1. 删除原来的远程仓库链接
git remote remove origin

# 2. 在GitHub上创建新仓库（比如叫 AuditionCopilot-Modified）
# 然后添加新的远程仓库
git remote add origin https://github.com/你的用户名/AuditionCopilot-Modified.git

# 3. 添加所有修改
git add .

# 4. 提交修改
git commit -m "修改游戏窗口名称为'劲舞团 华东一区'并添加GitHub Actions自动编译"

# 5. 推送到GitHub
git push -u origin main
```

## GitHub Actions 工作流程

推送代码后，GitHub会自动：

1. ✅ **检出代码** - 下载你的代码
2. ✅ **设置编译环境** - 配置MSBuild和NuGet
3. ✅ **还原依赖** - 下载所需的NuGet包
4. ✅ **编译Debug版本** - 编译调试版本
5. ✅ **编译Release版本** - 编译发布版本（推荐使用）
6. ✅ **上传编译产物** - 自动打包EXE和DLL文件

## 下载编译好的EXE

### 方式1：从Actions下载

1. 打开你的GitHub仓库
2. 点击顶部的 **"Actions"** 标签
3. 点击最新的workflow运行记录
4. 等待编译完成（大约2-5分钟）
5. 在页面底部找到 **"Artifacts"** 区域
6. 下载 **"AuditionCopilot-Release"** 压缩包
7. 解压后就能得到EXE文件

### 方式2：创建Release（推荐）

如果你想创建正式版本：

```bash
cd /root/AuditionCopilot

# 创建tag
git tag -a v1.0 -m "修改窗口名称为'劲舞团 华东一区'"

# 推送tag
git push origin v1.0
```

推送tag后，GitHub Actions会自动：
- 编译项目
- 创建GitHub Release
- 自动上传EXE和DLL文件
- 添加版本说明

然后你就可以在仓库的 **"Releases"** 页面直接下载EXE了！

## 触发编译的方式

GitHub Actions会在以下情况自动编译：

1. **推送到main/master分支** - 每次推送代码都会自动编译
2. **创建Pull Request** - 提交PR时自动编译测试
3. **创建tag** - 创建版本标签时编译并发布Release
4. **手动触发** - 在Actions页面点击"Run workflow"手动触发

## 查看编译状态

1. 打开GitHub仓库
2. 点击 **"Actions"** 标签
3. 查看最新的workflow运行状态：
   - 🟡 黄色圆圈 = 正在编译
   - ✅ 绿色对勾 = 编译成功
   - ❌ 红色叉号 = 编译失败

## 编译失败怎么办？

如果编译失败：

1. 点击失败的workflow
2. 查看详细的错误日志
3. 常见问题：
   - **NuGet包还原失败** - 网络问题，重新运行workflow
   - **编译错误** - 代码有语法错误，检查修改的代码
   - **找不到文件** - 路径配置问题，检查.yml文件

## 本地测试（可选）

如果你想在推送前测试GitHub Actions配置：

```bash
# 安装act工具（模拟GitHub Actions）
# 需要Docker环境
curl https://raw.githubusercontent.com/nektos/act/master/install.sh | sudo bash

# 在本地运行workflow
cd /root/AuditionCopilot
act -j build
```

## 注意事项

1. **首次编译时间较长** - 需要下载依赖包，大约5-10分钟
2. **后续编译更快** - GitHub会缓存依赖，2-3分钟即可完成
3. **Artifacts保留时间** - 编译产物默认保留90天
4. **私有仓库限制** - 免费账户每月有2000分钟的Actions时间限制

## 下一步

推送代码后：

1. ✅ 等待GitHub Actions编译完成
2. ✅ 下载编译好的EXE文件
3. ✅ 在Windows上测试运行
4. ✅ 如果需要修改，改完代码再推送，自动重新编译

## 快速命令总结

```bash
# 进入项目目录
cd /root/AuditionCopilot

# 添加所有修改
git add .

# 提交修改
git commit -m "修改游戏窗口名称并添加自动编译"

# 推送到GitHub
git push origin main

# （可选）创建Release版本
git tag -a v1.0 -m "首个修改版本"
git push origin v1.0
```

---

**配置完成！现在只要推送代码，GitHub就会自动帮你编译成EXE！**

有问题随时问老王我！
