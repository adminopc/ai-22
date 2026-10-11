# errors.md · 错题本

> 每天 5 分钟，一行一条：**报错原文 → 原因 → 解法**
> 零基础真正的瓶颈不是"学不会"，是同一个坑踩五次。
> 到 D19 加异常处理时，这本册子就是素材库。

---

## D1（2026-10-02 晚 ~ 10-03）

### 环境 / 虚拟环境

- `python -m venu` → 模块名拼错（venu 应为 venv） → 正确写法 `python -m venv venv`；报错头里露出的 python 路径说明 PATH 配置正常
- `\Python313\python.exe: No module named venu` → 同一条的完整报错原文 → 同上
- 激活后提示符是 `(venv) D:\code\` 而非 `(venv) D:\code\ai-22>` → cmd 开在了父目录 `D:\code`，venv 建到了错误位置 → venv 路径写死在 `pyvenv.cfg` / `Scripts\activate.bat` 里，**不能移动只能删了重建**；开 cmd 前先确认地址栏是目标文件夹

### 文件 / 目录

- `.gitignore` 建出来是**文件夹**（`dir /a` 左边有 `<DIR>`） → Windows 资源管理器不允许创建以点开头的文件名，右键新建只能选「文件夹」 → 用 VS Code 的「新建文件」；或记事本「另存为 + 文件名写 `".gitignore"`（带英文双引号）+ 保存类型选『所有文件』」
- 判断口诀：`dir /a` 条目左边有 `<DIR>` 是文件夹，显示字节数（如 40）才是文件

### Git

- `error: failed to push some refs to 'https://github.com/adminopc/ai-22'` → **本地一次成功的提交都没有**（漏了 `git add .`），commit 无功而返，push 没东西可推 → 补 `git add .` → `git status` → `git commit -m "D1 完成hello"` → 再 push。**与网络、认证、编码全都无关**
- `Nothing specified, nothing added.` + `hint: Maybe you wanted to say 'git add .'?` → 敲了 `git add`，漏掉末尾空格 + 英文句点 → 写 `git add .`（`.` ＝ 当前目录下全部文件）
- `git: 'add.' is not a git command.` → 敲了 `git add.`，`add` 和 `.` 之间漏了空格，git 把 `add.` 当成命令名 → `git`、`add`、`.` 是三个独立词，需要两个空格
- `warning: LF will be replaced by CRLF in hello.py` → Windows 换行符自动转换（`core.autocrlf=true`） → **是 warning 不是 error**，忽略即可

### 环境 / 认证

- 网页弹「确认访问」（sudo 模式）要求输入密码 → GitHub 账号密码忘记了 → 走「忘记密码了吗？」→ 邮箱收信（**记得翻垃圾箱**）→ 重置 → 重新授权；命令行 push 出现 `Authentication Succeeded` 即成功

---

## 判断口诀（越用越快）

| 看到什么 | 真问题 | 先做什么 |
|---|---|---|
| `git status` 显示 `No commits yet` | 缺提交，不是网络问题 | `git add .` |
| `! [rejected] ... (fetch first)` | 远程有你没有的提交 | `git pull --rebase origin main` |
| `Authentication failed` / 提示输密码 | 认证问题 | 用 Personal Access Token（**不能填账号密码**） |
| `No module named xxx` | 包没装 或 名字拼错 | 先看拼写，再 `pip install xxx` |
| "我明明装过这个包" | 不在虚拟环境里 | `venv\Scripts\activate` 重新激活 |

## 命令行的两条通用提醒

1. **每个"词"之间必须有空格**。`git` `add` `.` 是三个词。
2. **没输出＝成功**。以下命令干完活是不说话的：`git add .`、`python -m venv venv`、`git remote add origin ...`。
