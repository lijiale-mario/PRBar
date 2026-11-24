# PRBar

在 Mac 菜单栏里查看你在 GitHub 上开着的 PR。每个 PR 的 CI、Review、能否合并一眼就能看清，失败的 GitHub Actions job 可以直接点一下重跑。

- 点开菜单栏图标时刷新，不在后台轮询。
- CI 状态按每个 workflow 最新一次运行计算，已经被新运行取代的旧失败不算在内。
- 展开 PR 可以看到每个 check，按「失败 / 进行中 / 其他 / 通过」分区显示，点一下打开详情页。
- 失败的 GitHub Actions job 按 workflow run 一键重跑。其他来源的 check（比如 Vercel）只能查看状态，因为 GitHub 不允许用个人 token 重跑它们。
- 账号跟随 GitHub CLI 当前登录的账号，`gh auth switch` 之后再打开面板就会切过来。

## 下载

在 [Releases](../../releases/latest) 下载 `PRBar-<版本>.dmg`，打开后把 PRBar 拖进「应用程序」。已用 Developer ID 签名并通过 Apple 公证。需要 macOS 26 或更新版本。

## 使用前提

- 安装 [GitHub CLI](https://cli.github.com)（`gh`），并用 `gh auth login` 登录。PRBar 会在 `/opt/homebrew/bin/gh` 和 `/usr/local/bin/gh` 这两个位置查找 gh。
- 重跑 job 需要你对那个仓库有相应权限。没有权限时，GitHub 返回的错误会显示在那一组 check 下面。

## 隐私

PRBar 只和 `api.github.com` 通信：用 gh 当前账号的 token 查询你开的 PR 和 check 状态，以及发起重跑。token 每次刷新时从 gh 读取，不会保存，也不会发送到别的地方。不收集任何数据。
