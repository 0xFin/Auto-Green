# Auto-green

自动保持 GitHub 提交状态常绿

## 原理

使用 GitHub Actions 的定时任务功能，每隔一段时间自动执行 `git commit`，提交信息为 "a commit a day keeps your girlfriend away"

有关 Github Action 的原理，可查看官方文档 [Github Action 简介](https://docs.github.com/cn/actions/learn-github-actions/introduction-to-github-actions)

## 使用

- 点右上角 **Use this template** - **Create a new repository** 创建新仓库 **（ :warning: 不要 Fork，因为 Fork 项目的动态并不会让你变绿 :warning: ）**
- 修改 ci.yml 文件中的第 23 行邮箱为自己的 GitHub 邮箱账号
- (可选) 可以通过修改 ci.yml 文件的第 8 行来调整自动提交频率

## 频率设置

计划任务语法有 5 个字段，中间用空格分隔，每个字段代表一个时间单位

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

**注**：由于 GitHub Actions 的限制，如果设置为 `* * * * *` 实际的执行频率为每 5 分执行一次
