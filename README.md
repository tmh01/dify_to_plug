# 🚀 零基础保姆级教程：将 Dify 应用变成 Chrome / Edge 浏览器插件

如果你在 Dify 上做了一个好用的 AI 助手（比如论文检阅、翻译工具等），想要把它变成浏览器右上角随叫随到的插件，请严格按照以下步骤操作！

Edge 和 Chrome 浏览器内核相同，因此**一套代码，双端通用**！

---

## 🎯 第一步：获取你 Dify 应用的链接

1. 登录你的 Dify 后台。
2. 进入你想做成插件的应用（比如“论文检阅完整版”）。
3. 在页面上方或右上角，点击 **发布 (Publish)** -> **嵌入网站 (Embed)** 。
4. 找到类似 `https://udify.app/chat/xxxxxxxxx` 的公共链接。
5. **复制并保存**这个链接，接下来马上要用到。

---

## 📁 第二步：创建插件代码文件夹

在你的电脑桌面上，新建一个文件夹，命名为 `Dify_Extension`（名字随意）。
在这个文件夹里，我们只需要创建 **3个文件**。

### 1. 配置文件 (`manifest.json`)
在文件夹里新建一个文本文档，重命名为 `manifest.json`（注意后缀名必须是 `.json`，不能是 `.txt`）。
右键用**记事本**或 VS Code 打开它，**将编码另存为 UTF-8**（防止中文乱码），然后复制以下代码：

```json
{
  "manifest_version": 3,
  "name": "我的 Dify AI助手",
  "version": "1.0.0",
  "description": "基于 Dify 打造的专属浏览器 AI 助手，支持一键唤出对话。",
  "action": {
    "default_popup": "popup.html",
    "default_icon": "icon.png"
  },
  "icons": {
    "128": "icon.png"
  }
}
```

### 2. 弹窗界面 (`popup.html`)
新建第二个文件，命名为 `popup.html`。
同样用记事本打开，复制以下代码，并**把你第一步复制的 Dify 链接替换进去**！

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <style>
    /* 调整弹窗的大小，建议宽 400px，高 600px */
    body { width: 400px; height: 600px; margin: 0; padding: 0; overflow: hidden; }
    iframe { width: 100%; height: 100%; border: none; }
  </style>
</head>
<body>
  <!-- ⚠️ 务必将下面的 src 链接替换为你自己的 Dify 链接！ -->
  <iframe src="https://udify.app/chat/你的专属ID" allow="clipboard-read; clipboard-write; microphone"></iframe>
</body>
</html>
```

### 3. 准备插件图标 (`icon.png`)
找一张正方形的图片（建议尺寸 `128x128` 或 `300x300` 像素），命名为 `icon.png`，放进这个文件夹里。

> ✅ **检查一下**：现在你的文件夹里应该正好有这 3 个文件：`manifest.json`、`popup.html`、`icon.png`。

---

## 🔌 第三步：在浏览器中本地安装与测试

### 👉 如果你用的是 Edge 浏览器：
1. 在浏览器地址栏输入：`edge://extensions/` 并回车。
2. 看页面左侧（或右上角），打开 **“开发人员模式”** 开关。
3. 点击右上角的 **“加载解压缩的扩展”** 按钮。
4. 选中你桌面上刚才创建的那个 `Dify_Extension` 文件夹。
5. **最重要的一步**：安装成功后，点击浏览器右上角的**“拼图”图标**（扩展菜单），找到你的插件，点击旁边的**眼睛/图钉**把它固定在工具栏上。
6. 点击你的插件图标，你的 Dify 助手就会弹出来了！

### 👉 如果你用的是 Google Chrome 浏览器：
1. 在地址栏输入：`chrome://extensions/` 并回车。
2. 打开右上角的 **“开发者模式”**。
3. 点击左上角的 **“加载已解压的扩展程序”** 。
4. 选择你的文件夹。
5. 同样点击浏览器右上角的**拼图图标**，把它“固定 (Pin)”出来，点击即可使用。

---

## 📤 第四步：打包与发布商店（选做）

如果你想让朋友们一键安装，可以发布到商店：

1. 把 `Dify_Extension` 文件夹里的 3 个文件全选，**右键压缩成一个 `.zip` 文件**（注意不要多嵌套一层文件夹）。
2. **发布到 Edge 商店（完全免费）**：
   - 访问 [Microsoft Edge 合作伙伴中心](https://partner.microsoft.com/zh-cn/dashboard/microsoftedge/public/login) 。
   - 注册开发者账号 -> 创建新扩展 -> 上传 ZIP 包。
   - 填写名称和介绍（**千万不要在介绍里写“Chrome”字眼，否则会报���**）。
   - 隐私策略随便填一个公开文档链接，提交审核即可。
3. **发布到 Chrome 商店（需交 5 美元）**：
   - 访问 [Chrome 开发者控制台](https://chrome.google.com/webstore/devconsole/) 。
   - 缴纳 5 美元终身注册费。
   - 上传 ZIP 并填写信息，提交审核。