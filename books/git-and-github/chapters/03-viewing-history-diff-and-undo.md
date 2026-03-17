# 第三章：回看与回退——如何查看历史、比较差异并安全撤销

> 语言 / Language：**中文** | [English](03-viewing-history-diff-and-undo.en.md)

## 本章你会学到什么

- 如何查看 Git 的提交历史，找到你需要的那次提交
- 如何比较不同版本之间的差异
- 如何安全地撤销错误的修改
- 理解 `git restore`、`git reset`、`git revert` 三种撤销方式的区别
- 掌握在不同场景下选择正确的撤销方法

## 为什么需要学这个

想象一下这样的场景：

你正在写一篇文档，昨天还好好的，今天打开一看，某个段落突然变得很奇怪。你记得自己改过这里，但不记得具体改了什么。如果没有版本控制，你只能凭记忆慢慢回想，或者干脆重写。

但如果你用了 Git，这个问题就变得简单了：你可以查看历史记录，看看这个段落在过去几天里经历了什么变化，找到是哪次修改导致了问题，然后精准地撤销那次修改。

这就是 Git 的"时间旅行"能力——它不仅能记录你的每一次修改，还能让你随时回到过去，查看、比较、甚至撤销任何一次修改。

这种能力在以下场景中特别有用：

- **找 bug**：代码突然出问题了，你需要找到是哪次提交引入的 bug
- **对比版本**：你想看看这周和上周的文档有什么区别
- **撤销错误**：你不小心删除了重要内容，想要恢复
- **实验新想法**：你想尝试一个新方案，但又担心搞砸，需要随时能退回来

在这一章，我们会系统学习如何使用 Git 的这些"时间旅行"功能。

## 查看提交历史：Git 的时间线

### 这是什么

Git 的提交历史就像一条时间线，记录了你的项目从诞生到现在的每一次变化。每次你运行 `git commit`，Git 就会在这条时间线上添加一个新的节点，记录下当时的项目状态。

查看提交历史，就是沿着这条时间线往回看，了解项目是如何一步步演变到现在的样子的。

### 为什么需要它

提交历史不只是一份"日志"，它是你理解项目演进的关键工具：

- **追溯变化**：某个功能是什么时候加入的？
- **定位问题**：bug 是在哪次提交中引入的？
- **理解决策**：为什么当时要这样修改？（通过提交信息）
- **团队协作**：其他人最近做了什么修改？

### 怎么用

#### 最基本的用法：`git log`

打开终端，在你的 Git 仓库中运行：

```bash
$ git log
```

你会看到类似这样的输出：

```
commit 61b6377a8c9f2e4d3b1a5c6e7f8g9h0i1j2k3l4m
Author: Mark <mark@example.com>
Date:   Sun Mar 16 23:48:15 2026 +0800

    docs: add git chapter on working tree staging and first commit

commit 4d64e45b7c8d9e0f1a2b3c4d5e6f7g8h9i0j1k2l
Author: Mark <mark@example.com>
Date:   Sun Mar 16 20:30:42 2026 +0800

    docs: add beginner fast-track chapters and expand EN i18n content

commit 96ff8b5c6d7e8f9g0h1i2j3k4l5m6n7o8p9q0r1s
Author: Mark <mark@example.com>
Date:   Sat Mar 15 18:22:10 2026 +0800

    Humanize textbook content: remove formulaic patterns and AI-sounding phrases
```

每个提交包含四部分信息：

1. **commit ID**（提交 ID）：一串很长的字符，是这次提交的唯一标识
2. **Author**（作者）：谁做的这次提交
3. **Date**（日期）：什么时候提交的
4. **提交信息**：这次提交做了什么

#### 更简洁的视图：`git log --oneline`

如果你觉得默认的输出太啰嗦，可以用 `--oneline` 参数：

```bash
$ git log --oneline
```

输出会变成这样：

```
61b6377 docs: add git chapter on working tree staging and first commit
4d64e45 docs: add beginner fast-track chapters and expand EN i18n content
96ff8b5 Humanize textbook content: remove formulaic patterns and AI-sounding phrases
e737406 Humanize Git-and-GitHub volume: improve clarity, flow, and beginner accessibility
f2ca9ca Start Git and GitHub textbook volume
```

每行一个提交，只显示：
- 提交 ID 的前7位（足够用来识别了）
- 提交信息

这种格式特别适合快速浏览历史。

#### 可视化分支历史：`git log --graph`

如果你的项目有分支（我们会在第四章详细讲分支），可以用 `--graph` 参数来可视化：

```bash
$ git log --oneline --graph --all
```

输出会像这样：

```
* 61b6377 docs: add git chapter on working tree staging and first commit
* 4d64e45 docs: add beginner fast-track chapters and expand EN i18n content
* 96ff8b5 Humanize textbook content: remove formulaic patterns
* e737406 Humanize Git-and-GitHub volume
* f2ca9ca Start Git and GitHub textbook volume
```

`--all` 参数表示显示所有分支的历史，而不只是当前分支。

#### 查看具体改动：`git log -p`

如果你想看每次提交具体改了什么内容，可以用 `-p` 参数（p 代表 patch，补丁）：

```bash
$ git log -p
```

这会在每个提交信息后面显示详细的改动内容（类似 `git diff` 的输出）。

**注意**：这个命令的输出会非常长，适合用来查看最近几次提交的详细改动。你可以加上 `-2` 参数只看最近2次提交：

```bash
$ git log -p -2
```

#### 搜索特定提交：`git log --grep`

如果你记得提交信息中的某个关键词，可以用 `--grep` 来搜索：

```bash
$ git log --grep="chapter"
```

这会列出所有提交信息中包含"chapter"的提交。

#### 查看特定作者的提交：`git log --author`

如果你想看某个人的提交历史：

```bash
$ git log --author="Mark"
```

#### 查看单个提交的详细信息：`git show`

如果你想查看某个特定提交的详细信息，可以用 `git show`：

```bash
$ git show 61b6377
```

这会显示：
- 提交的完整信息（作者、日期、提交信息）
- 这次提交改动的详细内容

### 实战演练：找到引入 bug 的提交

**场景**：你发现文档中有个错误，想找到是哪次提交引入的。

**前置条件**：你有一个 Git 仓库，里面有一些提交历史。

**操作步骤**：

**第1步：查看最近的提交历史**

```bash
$ git log --oneline -10
```

输出：
```
61b6377 docs: add git chapter on working tree staging and first commit
4d64e45 docs: add beginner fast-track chapters
96ff8b5 Humanize textbook content
e737406 Humanize Git-and-GitHub volume
f2ca9ca Start Git and GitHub textbook volume
...
```

**第2步：如果你记得错误相关的关键词，用 grep 搜索**

假设错误和"staging"相关：

```bash
$ git log --grep="staging"
```

输出：
```
commit 61b6377a8c9f2e4d3b1a5c6e7f8g9h0i1j2k3l4m
Author: Mark <mark@example.com>
Date:   Sun Mar 16 23:48:15 2026 +0800

    docs: add git chapter on working tree staging and first commit
```

**第3步：查看这次提交的详细改动**

```bash
$ git show 61b6377
```

这会显示这次提交改了哪些文件、改了什么内容。你可以从中找到引入错误的具体位置。

**验证结果**：你找到了引入错误的提交，知道了是什么时候、谁、为什么引入的这个错误。

**可能遇到的问题**：

- **问题1**：`git log` 输出太多，看不过来
  - **解决**：用 `git log --oneline` 简化输出，或者用 `-10` 参数只看最近10次提交

- **问题2**：不记得关键词，不知道怎么搜索
  - **解决**：用 `git log -p` 查看详细改动，或者用 `git log --all --source -- <文件路径>` 查看某个文件的修改历史

## 比较差异：看看改了什么

### 这是什么

在 Git 中，"差异"（diff）指的是两个版本之间的不同。Git 可以帮你比较：
- 工作区和暂存区的差异
- 暂存区和最新提交的差异
- 任意两个提交之间的差异
- 某个文件在不同版本中的差异

这就像是在两份文档之间做"对比"，Git 会告诉你哪些行被添加了、哪些行被删除了、哪些行被修改了。

### 为什么需要它

比较差异是 Git 中最常用的操作之一：

- **提交前检查**：确认你即将提交的内容是否正确
- **理解变化**：看看某个文件从上周到现在改了什么
- **代码审查**：检查别人的修改是否合理
- **调试问题**：对比正常版本和有问题的版本，找出差异

### 怎么用

还记得第二章讲的 Git 三层模型吗？

```
工作区（Working Directory）
    ↓
暂存区（Staging Area）
    ↓
提交历史（Commit History）
```

`git diff` 就是用来比较这三层之间的差异的。

#### 比较工作区和暂存区：`git diff`

这是最常用的命令，用来查看"你刚刚修改了什么，但还没有 add"：

```bash
$ git diff
```

**场景**：你修改了一个文件，但还没有运行 `git add`，想看看自己改了什么。

假设你修改了 `README.md`，输出会像这样：

```diff
diff --git a/README.md b/README.md
index 1234567..abcdefg 100644
--- a/README.md
+++ b/README.md
@@ -1,4 +1,4 @@
 # 教材合集

-这是一个教材仓库。
+这是一个持续建设中的教材仓库，目标是把不同主题写成真正可读、可学、可复习的长期教材。
```

解读这个输出：
- `---` 开头的行：旧版本（暂存区中的版本）
- `+++` 开头的行：新版本（工作区中的版本）
- `-` 开头的行：被删除的内容（红色显示）
- `+` 开头的行：被添加的内容（绿色显示）

#### 比较暂存区和最新提交：`git diff --staged`

这个命令用来查看"你已经 add 了什么，即将 commit 的内容"：

```bash
$ git diff --staged
```

或者用它的别名：

```bash
$ git diff --cached
```

**场景**：你运行了 `git add`，想在 commit 之前再确认一下即将提交的内容。

#### 比较任意两个提交：`git diff <commit1> <commit2>`

你可以比较任意两个提交之间的差异：

```bash
$ git diff 61b6377 4d64e45
```

这会显示从提交 `61b6377` 到提交 `4d64e45` 之间的所有改动。

**提示**：你也可以用 `HEAD` 来代表最新的提交：

```bash
$ git diff HEAD~1 HEAD
```

`HEAD~1` 表示"最新提交的上一个提交"，所以这个命令会显示最近一次提交的改动。

#### 查看特定文件的差异

如果你只想看某个文件的差异，可以在命令后面加上文件路径：

```bash
$ git diff README.md
```

或者比较两个提交中某个文件的差异：

```bash
$ git diff 61b6377 4d64e45 README.md
```

### 实战演练：确认即将提交的内容

**场景**：你修改了几个文件，想在提交前确认一下改动是否正确。

**前置条件**：你已经修改了一些文件，有些已经 `git add`，有些还没有。

**操作步骤**：

**第1步：查看工作区的改动（还没 add 的）**

```bash
$ git diff
```

输出会显示所有还没有 add 的改动。

**第2步：查看暂存区的改动（已经 add 的）**

```bash
$ git diff --staged
```

输出会显示所有已经 add、即将 commit 的改动。

**第3步：如果发现问题，可以继续修改**

如果你发现某个改动不对，可以：
- 继续修改文件
- 重新 `git add`
- 再次用 `git diff --staged` 确认

**第4步：确认无误后提交**

```bash
$ git commit -m "docs: update README with project description"
```

**验证结果**：你清楚地知道自己提交了什么内容，避免了误提交。

**可能遇到的问题**：

- **问题1**：`git diff` 输出太多，看不清楚
  - **解决**：用 `git diff <文件路径>` 只看特定文件的差异

- **问题2**：不知道某个改动是在工作区还是暂存区
  - **解决**：先运行 `git status` 查看文件状态，再决定用 `git diff` 还是 `git diff --staged`

## 撤销操作：Git 的三种武器

### 这是什么

在 Git 中，"撤销"有很多种含义：
- 撤销工作区的修改（还没 add）
- 撤销暂存区的修改（已经 add，但还没 commit）
- 撤销已经提交的修改（已经 commit）
- 撤销已经推送的修改（已经 push）

Git 提供了三个主要的撤销命令：
1. **`git restore`**：撤销工作区或暂存区的修改（Git 2.23+ 新命令）
2. **`git reset`**：移动分支指针，重置暂存区和工作区
3. **`git revert`**：创建一个新提交来撤销旧提交

这三个命令的使用场景完全不同，选错了可能会导致数据丢失。

### 为什么需要它

人都会犯错：
- 不小心删除了重要内容
- 提交了不该提交的文件
- 提交信息写错了
- 整个功能开发方向错了

Git 的撤销功能就是你的"后悔药"，但你需要知道在什么情况下吃哪种药。

### 怎么用

#### 场景1：撤销工作区的修改（还没 add）

**情况**：你修改了一个文件，但还没有运行 `git add`，现在想撤销这些修改。

**命令**：

```bash
$ git restore <文件名>
```

或者撤销所有修改：

```bash
$ git restore .
```

**示例**：

```bash
# 1. 修改了 README.md
$ echo "错误的内容" >> README.md

# 2. 查看状态
$ git status

# 输出：
On branch main
Changes not staged for commit:
  modified:   README.md

# 3. 撤销修改
$ git restore README.md

# 4. 再次查看状态
$ git status

# 输出：
On branch main
nothing to commit, working tree clean
```

**注意**：`git restore` 会直接丢弃你的修改，无法恢复！使用前请确认。

**旧命令**：在 Git 2.23 之前，使用 `git checkout -- <文件名>`，现在不推荐使用。

#### 场景2：撤销暂存区的修改（已经 add，但还没 commit）

**情况**：你运行了 `git add`，但还没有 commit，现在想把文件从暂存区移除（但保留工作区的修改）。

**命令**：

```bash
$ git restore --staged <文件名>
```

**示例**：

```bash
# 1. 修改并添加到暂存区
$ echo "新内容" >> README.md
$ git add README.md

# 2. 查看状态
$ git status

# 输出：
On branch main
Changes to be committed:
  modified:   README.md

# 3. 从暂存区移除（但保留工作区的修改）
$ git restore --staged README.md

# 4. 再次查看状态
$ git status

# 输出：
On branch main
Changes not staged for commit:
  modified:   README.md
```

现在文件又回到了"已修改但未暂存"的状态。

**旧命令**：在 Git 2.23 之前，使用 `git reset HEAD <文件名>`。

#### 场景3：撤销已经提交的修改（还没 push）

这是最复杂的场景，有三种方法：`git reset` 的三种模式。

##### 方法1：`git reset --soft`（只移动 HEAD）

**效果**：撤销提交，但保留暂存区和工作区的修改。

**使用场景**：你想重新编辑提交信息，或者把多个提交合并成一个。

```bash
$ git reset --soft HEAD~1
```

`HEAD~1` 表示"当前提交的上一个提交"。

**示例**：

```bash
# 1. 查看提交历史
$ git log --oneline

# 输出：
abc1234 docs: add chapter 3
def5678 docs: add chapter 2

# 2. 撤销最近一次提交
$ git reset --soft HEAD~1

# 3. 查看状态
$ git status

# 输出：
On branch main
Changes to be committed:
  new file:   chapter-03.md
```

现在最近一次提交被撤销了，但文件还在暂存区，你可以重新提交。

##### 方法2：`git reset --mixed`（默认模式）

**效果**：撤销提交，重置暂存区，但保留工作区的修改。

**使用场景**：你想撤销提交，重新整理要提交的文件。

```bash
$ git reset HEAD~1
```

或者明确指定：

```bash
$ git reset --mixed HEAD~1
```

**示例**：

```bash
# 1. 撤销最近一次提交
$ git reset HEAD~1

# 2. 查看状态
$ git status

# 输出：
On branch main
Changes not staged for commit:
  modified:   chapter-03.md
```

现在文件回到了"已修改但未暂存"的状态。

##### 方法3：`git reset --hard`（最危险）

**效果**：撤销提交，重置暂存区和工作区，**完全丢弃所有修改**。

**使用场景**：你确定要完全放弃这次提交的所有内容。

```bash
$ git reset --hard HEAD~1
```

**警告**：这个命令会永久删除你的修改，无法恢复！使用前请三思。

**示例**：

```bash
# 1. 撤销最近一次提交并丢弃所有修改
$ git reset --hard HEAD~1

# 2. 查看状态
$ git status

# 输出：
On branch main
nothing to commit, working tree clean
```

所有修改都消失了。

##### 三种模式的对比

| 模式 | 移动 HEAD | 重置暂存区 | 重置工作区 | 使用场景 |
|------|-----------|------------|------------|----------|
| `--soft` | ✅ | ❌ | ❌ | 重新编辑提交 |
| `--mixed` | ✅ | ✅ | ❌ | 重新整理文件 |
| `--hard` | ✅ | ✅ | ✅ | 完全放弃修改 |

**记忆技巧**：
- `--soft`：最温柔，只动 HEAD
- `--mixed`：中等，动 HEAD 和暂存区
- `--hard`：最狠，全都动

#### 场景4：撤销已经推送的修改（已经 push）

**重要原则**：如果你已经把提交推送到远程仓库，**不要使用 `git reset`**！

为什么？因为 `git reset` 会改写历史，如果别人已经基于你的提交开始工作，你改写历史会导致他们的工作出问题。

**正确做法**：使用 `git revert`。

##### `git revert`：创建新提交来撤销

**效果**：创建一个新的提交，这个提交的内容是"撤销某个旧提交的修改"。

**使用场景**：撤销已经推送的提交。

```bash
$ git revert <提交ID>
```

**示例**：

```bash
# 1. 查看提交历史
$ git log --oneline

# 输出：
abc1234 docs: add wrong content
def5678 docs: add chapter 2

# 2. 撤销 abc1234 这次提交
$ git revert abc1234

# Git 会打开编辑器让你编辑提交信息，默认是：
# Revert "docs: add wrong content"
#
# This reverts commit abc1234.

# 3. 保存并退出编辑器

# 4. 查看提交历史
$ git log --oneline

# 输出：
xyz9012 Revert "docs: add wrong content"
abc1234 docs: add wrong content
def5678 docs: add chapter 2
```

注意：`git revert` 不会删除旧提交，而是创建一个新提交来"反向操作"。历史记录是完整的。

#### 场景5：找回"丢失"的提交（reflog）

**情况**：你不小心用 `git reset --hard` 删除了提交，想要找回来。

**命令**：`git reflog`

`reflog` 记录了你的 HEAD 指针的所有移动历史，即使提交被"删除"了，也能在 reflog 中找到。

**示例**：

```bash
# 1. 不小心删除了提交
$ git reset --hard HEAD~2

# 2. 查看 reflog
$ git reflog

# 输出：
def5678 HEAD@{0}: reset: moving to HEAD~2
abc1234 HEAD@{1}: commit: docs: add chapter 3
xyz9012 HEAD@{2}: commit: docs: add chapter 2

# 3. 找回被删除的提交
$ git reset --hard abc1234

# 或者用 HEAD@{1}
$ git reset --hard HEAD@{1}
```

现在提交又回来了！

**注意**：reflog 只保留最近几个月的记录（默认90天），所以不要指望它能找回很久以前的提交。

### 实战演练：撤销错误的提交

#### 实战1：撤销工作区的修改

**场景**：你正在写文档，不小心删除了一大段内容，还没有 add，想要恢复。

```bash
# 1. 不小心删除了内容
$ echo "" > important-file.md

# 2. 发现错误，立即撤销
$ git restore important-file.md

# 3. 验证文件已恢复
$ cat important-file.md
```

#### 实战2：撤销已经 add 但还没 commit 的修改

**场景**：你修改了多个文件并 add 了，但发现其中一个文件不应该提交。

```bash
# 1. 修改并添加多个文件
$ git add file1.md file2.md file3.md

# 2. 发现 file3.md 不应该提交
$ git restore --staged file3.md

# 3. 只提交 file1 和 file2
$ git commit -m "docs: update file1 and file2"
```

#### 实战3：撤销最近一次提交（还没 push）

**场景**：你提交了一个文件，但提交信息写错了。

```bash
# 1. 撤销提交，但保留修改
$ git reset --soft HEAD~1

# 2. 重新提交，使用正确的提交信息
$ git commit -m "docs: correct commit message"
```

#### 实战4：撤销已经 push 的提交

**场景**：你发现已经推送的提交有错误，需要撤销。

```bash
# 1. 使用 revert 创建撤销提交
$ git revert abc1234

# 2. 推送撤销提交
$ git push origin main
```

### 安全撤销的原则

#### 原则1：push 前可以用 reset，push 后只能用 revert

- **还没 push**：可以用 `git reset` 改写历史
- **已经 push**：必须用 `git revert` 创建新提交

#### 原则2：使用 `--hard` 前请三思

`git reset --hard` 会永久删除你的修改，使用前请确认：
- 你真的不需要这些修改了吗？
- 有没有备份？
- 能不能用 `--soft` 或 `--mixed` 代替？

#### 原则3：重要操作前先创建分支

如果你要做一个可能有风险的操作，先创建一个分支作为备份：

```bash
$ git branch backup-before-reset
$ git reset --hard HEAD~5
```

如果出问题了，可以切换回备份分支：

```bash
$ git checkout backup-before-reset
```

#### 原则4：记住 reflog 是最后的救命稻草

如果你真的搞砸了，记得用 `git reflog` 找回"丢失"的提交。

## 常见问题与解决

### 问题1：我不小心用 `git reset --hard` 删除了重要提交，怎么办？

**解决**：用 `git reflog` 找回。

```bash
$ git reflog
$ git reset --hard <提交ID>
```

### 问题2：我想撤销多次提交，应该怎么做？

**解决**：用 `git reset HEAD~N`，N 是你想撤销的提交数量。

```bash
# 撤销最近3次提交
$ git reset HEAD~3
```

### 问题3：`git revert` 时出现冲突，怎么办？

**解决**：手动解决冲突，然后继续 revert。

```bash
# 1. 解决冲突（编辑文件）
# 2. 添加解决后的文件
$ git add <文件名>
# 3. 继续 revert
$ git revert --continue
```

### 问题4：我想撤销某个文件的修改，但保留其他文件，怎么做？

**解决**：用 `git restore` 指定文件。

```bash
$ git restore <文件名>
```

### 问题5：`git restore` 和 `git reset` 有什么区别？

**解决**：
- `git restore`：用于撤销工作区或暂存区的修改，不影响提交历史
- `git reset`：用于移动 HEAD 指针，改变提交历史

简单记忆：
- 还没 commit → 用 `git restore`
- 已经 commit → 用 `git reset` 或 `git revert`

## 本章小结

在这一章，我们学习了 Git 的"时间旅行"能力：

1. **查看历史**：
   - `git log`：查看提交历史
   - `git log --oneline`：简洁视图
   - `git log --graph`：可视化分支
   - `git log -p`：查看详细改动
   - `git show`：查看单个提交

2. **比较差异**：
   - `git diff`：工作区 vs 暂存区
   - `git diff --staged`：暂存区 vs 最新提交
   - `git diff <commit1> <commit2>`：比较两个提交

3. **撤销操作**：
   - `git restore`：撤销工作区或暂存区的修改
   - `git reset --soft`：撤销提交，保留暂存区和工作区
   - `git reset --mixed`：撤销提交，保留工作区
   - `git reset --hard`：撤销提交，丢弃所有修改
   - `git revert`：创建新提交来撤销（用于已 push 的提交）
   - `git reflog`：找回"丢失"的提交

4. **安全原则**：
   - push 前可以用 reset，push 后只能用 revert
   - 使用 `--hard` 前请三思
   - 重要操作前先创建备份分支
   - 记住 reflog 是最后的救命稻草

## 下一步

现在你已经掌握了 Git 的基本操作：初始化、提交、查看历史、比较差异、撤销修改。

但到目前为止，我们都是在一条直线上工作——每次提交都是在上一次提交的基础上继续。

在下一章，我们会学习 Git 最强大的功能之一：**分支**。

分支让你可以同时进行多个"平行宇宙"的开发：
- 在一个分支上开发新功能
- 在另一个分支上修复 bug
- 在第三个分支上做实验

而且这些分支之间互不干扰，最后还能合并到一起。

这听起来很神奇，对吧？让我们在第四章揭开分支的秘密。
