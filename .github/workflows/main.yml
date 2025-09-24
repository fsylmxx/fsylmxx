# GitHub Action for generating a contribution graph with a snake eating your contributions
name: Generate Snake Animation

on:
  # 自动运行的频率 (设置为每天一次，避免过于频繁)
  schedule:
    - cron: "0 0 * * *"

  # 允许你手动触发运行
  workflow_dispatch:

  # 当代码被推送到主分支时运行
  push:
    branches:
      - main  # <-- 如果你的主分支是 master, 请把这里改成 master

jobs:
  generate:
    permissions:
      contents: write
    runs-on: ubuntu-latest
    timeout-minutes: 10

    steps:
      - name: Generate github-contribution-grid-snake.svg
        uses: Platane/snk/svg-only@v3
        with:
          # 自动获取你的 GitHub 用户名
          github_user_name: ${{ github.repository_owner }}

          # 定义输出的动画文件，这里会同时生成亮色和暗色两个版本
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark

      - name: Push generated files to the output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          # 这个 Action 会把生成的动画图片推送到一个名叫 'output' 的新分支
          target_branch: output
          build_dir: dist
        env:
          # GITHUB_TOKEN 是自动提供的，无需修改
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
