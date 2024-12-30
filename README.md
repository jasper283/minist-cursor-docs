# Minist 开发规范文档

## 开发环境
- Flutter SDK: 3.24.5

## 项目结构
```
- assets/    # 本地资源
  ├── images/    # 图片资源 (命名规则: a.png为浅色, a_dark.png为深色)
  └── translations/    # 多语言资源
- lib/
  ├── configuration/   # 常量、多语言、主题、资源、路由、API
  ├── model/          # 数据模型
  ├── pages/          # 页面
  ├── utils/          # 工具类
  └── widget/         # 组件类
```

## 开发规范

### 1. 状态管理 (Riverpod)
- 使用 ConsumerWidget 替代 StatelessWidget
- 使用 HookConsumerWidget 替代 StatefulWidget
- 优先使用 ref.watch() 监听状态变化
- 仅在需要调用方法时使用 ref.read()
- 异步数据必须使用 AsyncValue 处理加载、错误状态

### 2. 多语言开发
- 所有文案必须使用多语言key: `LK.xxx.l()`
- 参数化文案使用命名参数: `LK.message.l(namedArgs: {'key': 'value'})`
- 新增语言文案后运行: `dart run easy_localization:generate`

### 3. 主题规范
- 使用主题常量而非硬编码颜色值
- 文字样式使用 Theme.of(context).textTheme
- 支持动态切换明暗主题

### 4. 路由管理
- 统一使用 `MT.to()` 进行页面导航
- 路由名称统一在 RN 类中定义
- 支持命名路由和Widget导航两种方式

### 5. 网络请求
- 统一使用 Http 类处理请求
- API 地址统一在 Api 类中定义
- 必须处理请求错误和异常情况

### 6. UI 开发规范

#### 布局适配
- 使用 ScreenUtil 进行屏幕适配
- 尺寸单位：`.w`(宽度)、`.h`(高度)、`.r`(自适应)、`.sp`(字体)

#### 组件使用
- 图片加载统一使用 MTImage
- 弹窗使用 showMTDialog/showMTBottomSheet
- 列表优先使用 MTListView/MTScrollView
- 表单输入使用 MTTextField
- 按钮使用 MTButton

#### 性能优化
- 列表使用 KeepAliveView 维持状态
- 大列表必须使用 ListView.builder
- 合理使用 const 构造器
- 避免频繁重建，合理拆分组件

### 7. 数据存储
- 普通数据使用 Storage
- 敏感数据使用 SecureStorage
- 遵循数据分级存储原则

### 8. 工具类使用规范
- 日志打印使用 MTLog
- 设备信息通过 DeviceInfo 获取
- 权限管理统一通过 Permission 处理
- 防抖节流使用 DT 工具类

### 9. 代码风格
- 使用 trailing comma 改善格式化
- 遵循 80 字符行宽限制
- 优先使用 const 构造器
- 类成员顺序：构造函数 > 属性 > 生命周期 > 方法

### 10. 错误处理
- 异步操作必须使用 try-catch
- UI 层展示错误信息使用 SelectableText.rich
- 网络错误需要展示重试操作
- 空状态使用 BlankView 处理
