<p align="center">
  <a href="https://peifeng.li"><img width="184" alt="AVDB logo" src="https://github.com/li-peifeng/AVdb-Only/raw/refs/heads/main/public/logo.svg" /></a>
</p>
<p align="center">
  <a href="https://hub.docker.com/r/leolitaly/avdb"><img src="https://img.shields.io/docker/pulls/leolitaly/avdb?color=%2348BB78&logo=docker&label=pulls" alt="Docker pulls" /></a>
</p>

# Gfriends 女友头像仓库
![TotalNumber](https://img.shields.io/badge/全部女友数-325,365-blueviolet.svg)  ![AutoUpdate](https://img.shields.io/badge/更新日期-2026--10--11-brightgreen.svg)<br>

## 本仓库非官方库，属于 Avdb 和 Emby 插件 ActorArchives 的专有仓库， 使用和浏览请确认符合当地法律规定。

## 本地更新 Filetree.json

首次运行前安装图片元数据依赖：

```bash
python3 -m pip install Pillow
```

新增、删除或重命名 `Content/` 下的头像后，可以在本地运行：

```bash
./scripts/update_filetree_local.sh
```

脚本会按 GitHub Actions 使用的格式扫描 `Content/`，更新 `Filetree.json` 的 `Content` / `Information`，并同步 README 顶部的总数和更新日期 badge。图片值的格式为 `文件名?w=宽度&h=高度&t=缓存时间戳`；默认会保留已有条目的 `t`，并为缺少尺寸的条目补写 `w` / `h`。

如需重新读取全部图片尺寸：

```bash
./scripts/update_filetree_local.sh --refresh-dimensions
```

如需强制刷新全部时间戳：

```bash
./scripts/update_filetree_local.sh --refresh-timestamps
```

如果脚本提示有历史别名冲突，可追加 `--verbose` 查看具体跳过路径。

GitHub Actions 的自动更新也会调用同一个脚本：普通 push 只解析该次新增、替换、删除或重命名的图片；手动运行 `workflow_dispatch` 时会全量扫描并刷新尺寸。仓库仍使用浅克隆，并只额外获取普通 push 的起始提交。
