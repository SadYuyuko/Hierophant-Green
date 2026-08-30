# Github-auto-green

自动保持 GitHub 提交状态常绿（贴瓷砖）。

> A commit a day keeps life green.

## 原理

使用 GitHub Actions 的定时任务功能，每隔一段时间自动执行 `git commit`  
有关 Github Action 的原理，可查看官方文档 [Github Action 简介](https://docs.github.com/cn/actions/learn-github-actions/introduction-to-github-actions)

## 使用

- 点右上角 **Use this template** 按钮复制本 GitHub 仓库  
  :warning: 千万不要 Fork，因为 fork 项目的动态并不会让你变绿 :warning:  
- 修改 [ci.yml 文件的第 7、8 行](https://github.com/SadYuyuko/Hierophant-Green/blob/master/.github/workflows/ci.yml#L7-L8) 去掉前面的 `#` 号
- 修改 [ci.yml 文件的第 21、22 行](https://github.com/SadYuyuko/Hierophant-Green/blob/master/.github/workflows/ci.yml#L21-L22) 为自己的 GitHub 账号和昵称。由于commit记录默认可见，推荐账号填`数字+你的用户名@users.noreply.github.com`github隐私邮箱而不是个人邮箱
- (可选) 修改 [ci.yml 文件的第 8 行](https://github.com/SadYuyuko/Hierophant-Green/blob/master/.github/workflows/ci.yml#L8) 开启随机提交数量（1~10），使绿块有深浅变化

### 随机

默认每次只提交 1 次，绿块都为浅绿。若想让贴瓷砖有深浅变化，可在仓库 **Settings → Secrets and variables → Actions → Variables** 中新增变量：

| 变量名 | 取值 | 说明 |
| --- | --- | --- |
| `RANDOM_COMMIT` | `0` / `1` | `0` 或未设置时默认保持原样，改为 `1` 时每次随机提交 1~10 次，颜色深浅随机 |

## 频率

计划任务语法有 5 个字段，中间用空格分隔，每个字段代表一个时间单位。

```plain
┌───────────── 分钟 (0 - 59)
│ ┌───────────── 小时 (0 - 23)
│ │ ┌───────────── 日 (1 - 31)
│ │ │ ┌───────────── 月 (1 - 12 或 JAN-DEC)
│ │ │ │ ┌───────────── 星期 (0 - 6 或 SUN-SAT)
│ │ │ │ │
│ │ │ │ │
│ │ │ │ │
* * * * *
```

每个时间字段的含义：

|符号   | 描述        | 举例                                        |
| ----- | -----------| -------------------------------------------|
| `*`   | 任意值      | `* * * * *` 每天每小时每分钟                  |
| `,`   | 值分隔符    | `1,3,4,7 * * * *` 每小时的 1 3 4 7 分钟       |
| `-`   | 范围       | `1-6 * * * *` 每小时的 1-6 分钟               |
| `/`   | 每         | `*/15 * * * *` 每隔 15 分钟                  |

**注**：由于 GitHub Actions 的限制，如果设置为 `* * * * *` 实际的执行频率为每 5 分执行一次。
