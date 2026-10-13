# EduSkillBench paper

论文协作仓库，初始版本为 V4.1（2026-10-13，已修正框架图分叉箭头）。正文 8 页，含参考文献及附录的当前 PDF 共 20 页。主文件为根目录的 `main.tex`。

这是未定稿的私有协作版本，不是实验数据发布仓库。Qwen 最新汇总结果仍有逐题档案待核项，论文中的相应说明保留。

## 内容

```text
main.tex                 # 主文件，控制章节顺序
references.bib           # 参考文献
sections/                # 正文与附录
tables/                  # 论文实际引用的表格行
figures/                 # 四张预生成的矢量 PDF 图
acl.sty, acl_natbib.bst   # 原样保留的 ACL 模板文件
preview/main.pdf         # 最近一次人工确认的 PDF 快照
INITIAL_IMPORT.json      # 初始导入文件哈希与正文页码
```

38 个编译依赖从已有论文原样导入。没有模型权重、实验日志、原始答卷、API key、服务器凭据或无关项目。初始导入清单记录的是起点，不要求后续协作修改保持旧哈希。

## 在 Overleaf 中使用

1. 项目所有者在 Overleaf 账号设置连接 GitHub。
2. 选择 **New project → GitHub repo**，导入 `Chansl-Lucky/EduSkillBench-paper`。
3. 主文件选择 `main.tex`；建议先选 **XeLaTeX**，与本地已验收的 XeTeX 路径接近。
4. 编译后检查正文是否仍在 8 页内。不同 TeX Live 版本可能影响分页。`preview/main.pdf` 只是快照，不会随 `.tex` 自动更新。

GitHub 同步需要 Overleaf Premium 或适用的机构授权，且需要在项目 **Integrations → GitHub** 中手动 Pull / Push，不是刷新页面自动同步。已有 Overleaf 项目与已有 GitHub 仓库不能直接互相绑定；当前仓库建议通过上述“从 GitHub 新建项目”导入。[Overleaf 官方说明](https://docs.overleaf.com/integrations-and-add-ons/git-integration-and-github-synchronization/github-synchronization)

没有 Premium 时可以把本仓库的源码 ZIP 作为新项目上传，但这不构成持续 Git 同步。

## 日常协作顺序

**老师先在 Overleaf 修改时：**先用 Overleaf 的 GitHub 集成 Push，再在本地更新：

```sh
git status
git pull --ff-only origin main
```

**本地改稿后：**先编译和检查差异，只暂存这次明确修改的文件，再提交、推送；随后在 Overleaf 的 GitHub 集成里 Pull。

```sh
git diff
git add sections/introduction.tex
git commit -m "Clarify the introduction"
git push origin main
```

不要强制覆盖远端。遇到冲突先保留双方修改再合并。老师集中批注或开 Track Changes 时，先约定同步时点；跨 GitHub 拉取可能影响评论与修订标记的位置。[同步注意事项](https://docs.overleaf.com/integrations-and-add-ons/git-integration-and-github-synchronization/github-synchronization)

## 本地编译

有 TeX Live 和 `latexmk` 时：

```sh
make pdf
```

生成的工作 PDF 是根目录 `main.pdf`（不进入 Git）；确认通过后可用 `make preview` 更新需要提交的预览快照。四张图直接使用 PDF，无须 Python、额外模型或 shell escape。

模板来自 [ACL 官方样式仓库](https://github.com/acl-org/acl-style-files)。保留模板原有版权和许可声明；本仓库未修改 ACL 字号、边距及样式文件。
