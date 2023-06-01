# Hugo博客开启Giscus评论功能


[Giscus](https://giscus.app/)是利用[GitHub Discussions](https://docs.github.com/en/discussions)实现的评论系统，让访客借助 GitHub 在你的网站上留下评论和反应。

- 开源。🌏
- 无跟踪，无广告，永久免费。📡 🚫
- 无需数据库。所有数据均储存在 GitHub Discussions 中。:octocat:
- 支持自定义主题！🌗
- 支持多种语言。🌐
- 高可配置性。🔧
- 自动从 GitHub 拉取新评论与编辑。🔃
- 可自建服务！🤳

<!--more-->

## 准备工作

1. 你应该拥有一个公开类型的Github仓库，否则访客将无法查看 discussion。
2. Discussions 功能已在你的仓库中启用。
3. 你需要安装 [Giscus App](https://github.com/apps/giscus)，使其有权限访问对应仓库。

在完成以上步骤后，请前往 [Giscus 页面](https://giscus.app/) 获得你的设置。

在页面中找到以下配置项：

![giscus_config_editor.png](/img/tutorial/giscus_config_editor.png)

依次填写`仓库`、`页面 ↔️ discussion 映射关系`、`Discussion 分类`、`特性`、`主题`，之后滚动到页面下部的 “启用 giscus” 部分，如下图所示：

![Giscus配置](/img/tutorial/giscus_config.png)

## 配置

复制 `data-repo`, `data-repo-id`, `data-category` 和 `data-category-id` 四项，填入你的配置中，因为它们是必须的。

以基于hugo的Fixit主题为例：

```toml
[params]
  [params.page]
    [params.page.comment]
      [params.page.comment.giscus]
        enable = true
        repo = "zhang-weiming/zhang-weiming.github.io"  # Giscus的data-repo字段
        repoId = "R_xxxxxxxxxx"                         # Giscus的data-repo-id字段
        category = "General"                            # Giscus的data-category字段
        categoryId = "DIC_xxxxxxxxxxxxxxxx"             # Giscus的data-category-id字段
        mapping = "pathname"                            # Giscus的data-mapping字段
        strict = "0"                                    # Giscus的data-strict字段
        term = ""
        reactionsEnabled = "1"
        emitMetadata = "0"
        inputPosition = "bottom" # ["top", "bottom"]
        lightTheme = "light"
        darkTheme = "dark_dimmed"
        lazyLoad = true
```


---

> 作者: [张大锅](https://zhang-weiming.github.io/)  
> URL: https://zhang-weiming.github.io/post/tutorial/hugo_giscus/  

