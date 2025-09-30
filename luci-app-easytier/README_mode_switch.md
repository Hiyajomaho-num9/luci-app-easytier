# EasyTier 简易模式和高级模式切换功能

## 功能概述

为 EasyTier LuCI 插件添加了简易模式和高级模式的切换功能，让用户可以根据需要在简化界面和完整功能界面之间进行切换。

## 实现的功能

### 1. 模式切换按钮
- 在"启用"选项下方添加了"Switch Mode"按钮
- 按钮颜色和文字会根据当前模式动态变化
- 简易模式：绿色按钮显示"Simple Mode"
- 高级模式：蓝色按钮显示"Advanced Mode"

### 2. 简易模式功能
在简易模式下：
- **隐藏高级设置**：隐藏"Advanced Settings"标签页及其所有内容
- **隐藏上传程序**：隐藏"Upload Program"标签页及其所有内容  
- **隐藏自建Web服务器**：隐藏"Self-hosted Web Server"整个部分
- **简化基本设置**：在General Settings中只保留以下元素：
  - Enable（启用）
  - Restart（重启）
  - Network Name（网络名称）
  - Network Secret（网络密钥）
  - Peer Nodes（对等节点）
  - Hostname（主机名）
  - Enable DHCP（启用DHCP）
  - Interface IP Address（接口IP地址，当DHCP启用时隐藏）

### 3. 强制默认值
在简易模式下自动设置：
- **Startup Method**：强制设置为"Default"
- **Enable DHCP**：强制启用（设置为1）
- 当DHCP启用时，自动隐藏"Interface IP Address"字段

### 4. 状态持久化
- 使用localStorage保存用户的模式选择
- 页面刷新后保持用户选择的模式
- 支持多种页面加载方式的初始化

## 技术实现

### 文件结构
```
luasrc/
├── model/cbi/easytier.lua          # 主配置文件，添加模式切换按钮
└── view/easytier/mode_switch.htm   # 模式切换模板，包含JavaScript逻辑

po/
├── zh_Hans/easytier.po             # 中文翻译文件
└── templates/easytier.pot          # 翻译模板文件
```

### 关键技术点

1. **JavaScript 实现**：
   - 使用 localStorage 保存模式状态
   - 动态查找和隐藏/显示页面元素
   - 支持多种选择器策略确保兼容性
   - 使用 MutationObserver 监听DOM变化

2. **元素查找策略**：
   - 按name属性查找表单元素
   - 按文本内容查找标签页
   - 支持中英文界面自动适配
   - 查找最近的容器元素进行显示/隐藏

3. **样式优化**：
   - 添加CSS过渡效果
   - 按钮悬停效果
   - 统一的视觉风格

## 使用方法

1. 用户在EasyTier配置页面可以看到"Switch Mode"按钮
2. 点击按钮在简易模式和高级模式之间切换
3. 简易模式下只显示基本必需的配置选项
4. 高级模式下显示所有配置选项
5. 模式选择会自动保存，页面刷新后保持

## 兼容性

- 支持中英文界面
- 兼容不同版本的LuCI框架
- 支持各种浏览器的localStorage功能
- 响应式设计，适配不同屏幕尺寸

## 多语言支持

已添加以下翻译条目：
- Switch Mode / 切换模式
- Simple Mode / 简易模式  
- Advanced Mode / 高级模式
- Switch between Simple Mode and Advanced Mode / 在简易模式和高级模式之间切换