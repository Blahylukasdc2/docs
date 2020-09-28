---
title: 关于 Git Large File Storage
intro: '{{ site.data.variables.large_files.product_name_short }} 允许您向 {{ site.data.variables.product.product_name }} 推送大于 Git 推送限制的文件。'
redirect_from:
  - /articles/about-large-file-storage/
  - /articles/about-git-large-file-storage
versions:
  free-pro-team: '*'
  enterprise-server: '*'
---

{{ site.data.variables.large_files.product_name_short }} 处理大文件的方式是存储对仓库中文件的引用，而不实际文件本身。 为满足 Git 的架构要求，{{ site.data.variables.large_files.product_name_short }} 创建了指针文件，用于对实际文件（存储在其他位置）的引用。 {{ site.data.variables.product.product_name }} 在仓库中管理此指针文件。 克隆仓库时，{{ site.data.variables.product.product_name }} 使用指针文件作为映射来查找大文件。

{% if currentVersion == "free-pro-team@latest" %}
使用 {{ site.data.variables.large_files.product_name_short }}，可以将文件存储到：

| 产品                                                     | 最大文件大小           |
| ------------------------------------------------------ | ---------------- |
| {{ site.data.variables.product.prodname_free_user }} | 2 GB             |
| {{ site.data.variables.product.prodname_pro }}         | 2 GB             |
| {{ site.data.variables.product.prodname_team }}        | 4 GB             |
| {{ site.data.variables.product.prodname_ghe_cloud }} | 5 GB |{% else %}
 使用 {{ site.data.variables.large_files.product_name_short }}，可在仓库中存储的最大文件量：
{% if currentVersion ver_lt "enterprise-server@2.21" %}{{ site.data.variables.large_files.max_lfs_size }}{% else %}5 GB{% endif %}。
{% endif %}

您也可以将 {{ site.data.variables.large_files.product_name_short }} 与 {{ site.data.variables.product.prodname_desktop }} 结合使用。 有关在 {{ site.data.variables.product.prodname_desktop }} 中克隆 Git LFS 仓库的更多信息，请参阅"[将仓库从 GitHub 克隆到 GitHub Desktop](/desktop/guides/contributing-to-projects/cloning-a-repository-from-github-to-github-desktop)"。

{{ site.data.reusables.large_files.can-include-lfs-objects-archives }}

#### 指针文件格式

{{ site.data.variables.large_files.product_name_short }} 的指针文件看起来像：

```
version {{ site.data.variables.large_files.version_name }}
oid sha256:4cac19622fc3ada9c0fdeadb33f88f367b541f38b89102a3f1261ac81fd5bcb5
size 84977953
```

它会跟踪所用 {{ site.data.variables.large_files.product_name_short }} 的 `version`，后接文件的唯一标识符 (`oid`)。 它还会存储最终文件的 `size`。

{% tip %}

**提示**：{{ site.data.variables.large_files.product_name_short }} 不能用于 {{ site.data.variables.product.prodname_pages }} 站点。

{% endtip %}

### 延伸阅读

- "[使用 {{ site.data.variables.large_files.product_name_long }} 进行协作](/articles/collaboration-with-git-large-file-storage)"