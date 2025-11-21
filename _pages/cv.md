---
layout: single
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

## 使用 Google Drive 上传 CV（推荐）

为了方便上传并自动保存到 Google Drive，推荐使用 Google 表单的「文件上传」问题把 CV 保存到你的 Google Drive。优点：不需要把仓库写权限给外部人员；文件会存放在你自己的 Drive 中，便于管理。

步骤（一次性设置，站点访客可以通过该表单上传文件；上传者需要 Google 账号）：

1. 登录你的 Google 账号，打开 Google 表单（https://forms.google.com）。
2. 创建新表单，添加题目（例如："Upload CV"）。
3. 添加一个题型为“文件上传”的问题（Forms 会提示你文件将上传到表单所有者的 Drive）。
   - 可设置最大文件大小与允许的文件类型（选择 PDF）。
4. 在右上角点击“发送”，选择链接或嵌入 HTML（< >），复制表单的嵌入链接或公开链接。
5. 将该表单的嵌入链接粘贴到下面的 iframe `src` 属性中（或直接点击链接打开表单）。

示例嵌入（将 `GOOGLE_FORM_EMBED_URL` 替换为你从 Google 表单获得的嵌入 URL）：

<iframe src="GOOGLE_FORM_EMBED_URL" width="100%" height="900" frameborder="0" marginheight="0" marginwidth="0">正在加载…</iframe>

或者直接提供外部链接：

<p>表单链接（示例）： <a href="GOOGLE_FORM_LINK" target="_blank" rel="noopener">在新窗口打开上传表单</a></p>

说明与注意事项：
- 上传者需要登录 Google 账户才能上传文件（这是 Google 表单文件上传的限制）。
- 文件会保存在你的 Google Drive 中，表单会在 Drive 中创建一个文件夹来存放上传的文件。你可以在 Drive 中右上角选择“共享”以调整访问权限。
- 如果你希望在站点上展示最新的 CV（例如 `/files/CV.pdf`），可以在 Drive 中将该 PDF 设置为公开并使用公开链接或把文件下载到仓库中。

需要我为你把 Google 表单嵌入链接填上（如果你把表单链接发给我），或者我可以帮你生成一个简单的帮助文档说明如何创建表单并获取嵌入代码。 

