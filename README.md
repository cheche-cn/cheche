# 应用示例预览图片设置指南

## 设置"车车"示例的房子图片预览

如果你想把"车车"示例中生成的房子图片设置为应用示例的预览图片，可以通过以下两种方法：

### 方法一：使用预览图片更新工具（推荐）

1. 访问预览图片更新工具页面：[/tools/preview-updater](/tools/preview-updater)
2. 工具会自动搜索并选中"车车"应用示例
3. 在"预览图片URL"输入框中输入已生成的房子图片的URL
   - 如果是通过ComfyUI生成的图片，URL格式通常是：`/api/preview-image?filename=房子图片的文件名.png`
   - 也可以使用外部图片URL，例如：`https://example.com/house.jpg`
4. 点击"更新预览图片"按钮
5. 更新成功后，前往首页查看效果，"车车"示例应该显示房子图片

### 方法二：直接修改配置文件

如果你有权限直接访问服务器文件系统，可以按照以下步骤手动修改：

1. 找到`saved_playgrounds`目录下的"车车"示例配置文件，通常命名为`车车.json`
2. 打开该文件，找到`viewComfyJSON`对象
3. 在`viewComfyJSON`对象中添加或修改`previewImages`数组：
   ```json
   "viewComfyJSON": {
     "title": "车车",
     "previewImages": ["/api/preview-image?filename=你的房子图片.png"]
   }
   ```
4. 保存文件
5. 刷新首页，应该能看到更新后的预览图片

## 预览图片显示规则

- 应用示例会优先使用`previewImages`数组中的第一个有效图片URL作为预览图
- 如果没有有效的预览图URL，则会使用默认的占位图片
- 预览图片的类别标签会根据应用示例的标题自动判断，例如："车车"示例会自动标记为"建筑设计"类别

## 其他说明

- 预览图片更新后，需要刷新页面才能看到效果
- 上传的图片尺寸推荐为300x200像素或相近比例，以获得最佳显示效果
- 如果你的图片不是公开可访问的，建议先上传到服务器的公共目录，再使用相对路径

# 图像对比功能使用指南

## 什么是图像对比功能

图像对比功能允许你通过交互式滑块直观地比较两张图片的差异。这对于查看 AI 生成前后的变化、不同参数设置的效果对比或展示处理前后的变化非常有用。

## 如何使用图像对比功能

### 查看已有的图像对比示例

1. 在首页点击"对比展示"标签页
2. 可以查看现有的图像对比示例
3. 通过拖动滑块可以调整两张图片的显示比例
4. 点击"查看详情"按钮可以打开详情页面，查看更多信息

### 为现有应用创建图像对比效果

要为现有应用创建图像对比效果，你需要上传两张图片作为预览图：

1. 访问预览图片更新工具页面：[/tools/preview-updater](/tools/preview-updater)
2. 选择要添加对比效果的应用示例
3. 在"预览图片URL"输入框中输入第一张图片的URL，点击"更新预览图片"按钮
4. 然后再次输入第二张图片的URL，再次点击"更新预览图片"按钮
5. 系统会自动将两张图片添加到该应用的预览图数组中
6. 打开该应用的详情页，即可看到图像对比效果

### 使用技巧

- 左侧图片通常用于显示"处理前"或"原始图像"
- 右侧图片通常用于显示"处理后"或"优化图像"
- 图像对比滑块可以精确地拖动到任意位置，方便对比细节差异
- 在小屏设备上，可以使用触摸手势拖动滑块

## 典型应用场景

图像对比功能适用于以下场景：

1. **前后效果对比**：展示AI生成前后的差异
2. **参数调整对比**：对比不同参数设置下生成的结果
3. **版本效果对比**：比较不同AI模型版本生成的差异
4. **处理步骤对比**：展示图像处理不同阶段的变化

## 添加对比标签

如果你希望将某个应用示例添加到"对比展示"标签页中，可以在创建应用时将其标题命名为包含"对比"字样的名称，系统会自动将其归类到对比展示类别。

## OpenAI API配置指南（中国用户适用）

由于网络限制，中国用户在使用OpenAI API时需要进行特殊配置。以下是配置步骤：

### 1. 获取OpenAI API密钥

1. 前往 [OpenAI平台](https://platform.openai.com/) 注册/登录账号
2. 进入 API Keys 页面: https://platform.openai.com/api-keys
3. 点击 "Create new secret key" 创建新的密钥
4. 保存生成的密钥（仅显示一次）

### 2. 配置环境变量

在项目根目录创建或编辑 `.env.local` 文件，添加以下配置：

```bash
# OpenAI API配置
OPENAI_API_KEY=your_openai_api_key_here
NEXT_PUBLIC_OPENAI_API_IS_SET=true

# API代理配置 (解决中国大陆网络问题)
# 以下为常用的API代理服务，取消注释其中一个即可使用
OPENAI_API_BASE_URL=https://api.openai-proxy.com/v1
# OPENAI_API_BASE_URL=https://api.chatanywhere.com.cn/v1
# OPENAI_API_BASE_URL=https://api.closeai-proxy.xyz/v1

# 超时设置（毫秒）
OPENAI_API_TIMEOUT=60000

# 请求配置
OPENAI_API_MAX_RETRIES=3

# 调试模式
NEXT_PUBLIC_DEBUG_MODE=false
```

### 3. 支持的OpenAI模型

本项目使用以下OpenAI模型：

#### 聊天模型
- **gpt-4.1** (默认): OpenAI最新的顶级聊天模型
- **gpt-4-vision-preview**: 具有图像理解能力的模型
- **gpt-3.5-turbo**: 高性能与速度平衡的模型

#### 图像模型
- **gpt-image-1**: OpenAI最新的图像处理和生成模型
- **dall-e-3**: 用于图像生成的模型

### 4. 代理服务推荐

中国用户可以使用以下几种方式访问OpenAI API：

#### 方案一：第三方API代理服务（推荐新手）

以下是一些可靠的API代理服务：

- [API2D](https://api2d.com/)
- [OpenAI-SB](https://openai-sb.com/)
- [CloseAI](https://console.closeai-proxy.xyz/)
- [ChatAnywhere](https://chat-anywhere.cn/)

使用方法：注册账号，充值后获得API密钥，然后配置`OPENAI_API_BASE_URL`和`OPENAI_API_KEY`。

#### 方案二：自建代理服务器

如果有国外服务器，可以使用开源项目自建代理：

- [OpenAI Proxy](https://github.com/justjavac/openai-proxy)
- [FastGPT](https://github.com/labring/FastGPT)

#### 方案三：使用开发者工具代理

- 使用[Clash](https://github.com/Dreamacro/clash)、[V2Ray](https://github.com/v2ray/v2ray-core)等工具
- 为开发环境设置全局代理

### 5. 常见问题排查

如果遇到API连接问题，请检查：

1. API密钥是否正确设置
2. 代理配置是否有效
3. 账户余额是否充足
4. 模型名称是否准确(请使用`gpt-4.1`而非`gpt-4-turbo`)
5. 查看控制台网络请求错误信息

错误信息及解决方案：
- `model_not_found`: 模型名称错误或无权访问，检查模型名称是否正确
- `insufficient_quota`: 账户余额不足，需要充值
- `rate_limit_exceeded`: 请求频率过高，减少请求频率或等待一段时间

### 6. 本地开发测试

启动开发服务器进行测试：

```bash
npm run dev
```

访问 http://localhost:3000/openai 测试API连接和功能是否正常。

## RunningHub API集成

从v0.1.1版本开始，MercuryUI增加了对[RunningHub](https://www.runninghub.cn/)云端ComfyUI的支持。这使您能够利用RunningHub的云端GPU资源来运行ComfyUI工作流，无需本地安装和配置ComfyUI。

### 配置RunningHub API

要使用RunningHub API，您需要在`.env`文件中设置以下环境变量：

```bash
# RunningHub API配置
COMFYUI_SECURE="true"
COMFYUI_API_URL="www.runninghub.cn/api"
RUNNINGHUB_API_KEY="您的RunningHub API密钥"
RUNNINGHUB_WORKFLOW_ID="您要使用的工作流ID"
```

### 获取RunningHub API密钥和工作流ID

1. 注册成为RunningHub用户并开通基础会员权益（注意：免费用户不能使用RunningHub API）
2. 登录RunningHub网站，点击右上角头像 -> API控制台，即可找到您的API密钥
3. 工作流ID可以从您要使用的工作流URL中获取，例如`https://www.runninghub.cn/#/workflow/1850925505116598274`中的`1850925505116598274`

### 运行方式

当您在`.env`文件中正确配置RunningHub后，MercuryUI会自动检测并使用RunningHub API运行工作流，无需额外配置。系统会根据配置环境自动在本地ComfyUI和RunningHub云端之间切换。

### 使用限制

- 仅基础会员及以上权限可以使用RunningHub API
- API调用会消耗您账户的RH币，消耗费率与在网站上运行工作流一致
- 如需并发使用API，请参考RunningHub官方文档
