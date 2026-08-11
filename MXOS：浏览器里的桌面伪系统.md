标题: MXOS：浏览器里的桌面伪系统
日期: 2026年7月10日
分类: 项目发布
标签: MXOS, WebOS, 桌面系统, 前端, 喜灰之最

MXOS 是一个运行在浏览器里的桌面风格伪操作系统，也是我与喜灰之最的喜 PCOS 联动项目之一。它使用 HTML、CSS 和 JavaScript 模拟了桌面环境，支持多窗口、应用安装和一套简单的应用开发 API。

项目源码托管在 GitHub：[https://github.com/mangchenofficial/MXOS](https://github.com/mangchenofficial/MXOS)

## 一、MXOS 是什么

MXOS 的目标是在浏览器里提供一个接近真实桌面系统的体验：

- 桌面壁纸与图标
- 多窗口同时打开
- 任务栏与窗口管理
- 可安装第三方应用
- 应用运行在自己的窗口中

它完全基于前端技术，不需要后端服务，部署到 GitHub Pages 或任何静态托管平台都能直接运行。

## 二、应用包格式 .mx

MXOS 定义了自己的应用包格式 `.mx`，本质上是一个 ZIP 压缩包，里面包含：

```
app_name.mx
├── manifest.json      # 应用清单（必需）
├── manifest.xml       # XML 格式清单（可选，二选一）
├── app.bin            # 主程序 JavaScript（必需）
├── lib/               # 依赖库（可选）
├── assets/            # 资源文件（可选）
├── metadata/          # 图标、描述等元数据（可选）
└── signature.sig      # 数字签名（可选）
```

制作 `.mx` 应用只需要：

1. 创建包含上述文件的文件夹
2. 压缩为 ZIP
3. 把扩展名改为 `.mx`
4. 在 MXOS 中拖放安装

### manifest.json 示例

```json
{
  "id": "com.example.app",
  "name": "应用名称",
  "version": "1.0.0",
  "description": "应用描述",
  "icon": "📱",
  "author": "你的名字"
}
```

## 三、应用开发 API

MXOS 为第三方应用提供了一套简单的 JavaScript API。

### 窗口操作

```javascript
MXOS.setWindowTitle("新标题");
MXOS.setWindowSize(800, 600);
MXOS.minimizeWindow();
MXOS.maximizeWindow();
MXOS.closeWindow();
```

### 本地存储

```javascript
MXOS.Storage.set("key", "value");
const value = MXOS.Storage.get("key");
MXOS.Storage.remove("key");
```

### 通知与对话框

```javascript
MXOS.Notification.show({
    title: "提示",
    message: "操作完成",
    icon: "✅",
    duration: 3000
});

const result = await MXOS.Dialog.confirm("确定删除？", "此操作不可撤销");
```

### 网络请求

```javascript
const data = await MXOS.Network.fetch("https://api.example.com/data");
const ws = MXOS.Network.WebSocket("wss://api.example.com/ws");
```

## 四、透明背景设计

MXOS 的窗口默认使用透明背景，配合毛玻璃效果：

```css
.window {
    background: transparent;
    backdrop-filter: blur(30px) saturate(180%) brightness(1.1);
    border: 1px solid rgba(255, 255, 255, 0.1);
}
```

应用内容区域建议使用半透明白色背景提高可读性：

```css
.container {
    background: rgba(255, 255, 255, 0.05);
    backdrop-filter: blur(10px);
    border-radius: 8px;
    padding: 20px;
}
```

## 五、内置示例应用

MXOS 文档中提供了几个示例应用：

- **记事本**：使用 `MXOS.Storage` 保存文本内容
- **计算器**：基础四则运算
- **图片查看器**：加载本地图片并浏览

这些示例展示了 MXOS API 的基本用法，可以作为开发自己应用的起点。

## 六、与喜灰之最的喜 PCOS、NeoUI 的关系

MXOS 和 NeoUI 都是我与喜灰之最的喜 PCOS 联动的项目：

- **MXOS**：桌面端伪系统，强调多窗口和应用生态
- **NeoUI**：手机端伪系统，强调锁屏、桌面、移动应用体验

两者都基于浏览器前端技术，未来可能会共享应用格式或设计资源。

## 七、体验方式

可以直接访问 GitHub 仓库获取源码：

```bash
git clone https://github.com/mangchenofficial/MXOS.git
```

仓库包含 `MXOS.html` 主文件和完整的应用开发文档 `APP_DEVELOPMENT.md`。
