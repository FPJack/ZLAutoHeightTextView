# ZLAutoHeightTextView

[![CI Status](https://img.shields.io/travis/fanpeng/ZLAutoHeightTextView.svg?style=flat)](https://travis-ci.org/fanpeng/ZLAutoHeightTextView)
[![Version](https://img.shields.io/cocoapods/v/ZLAutoHeightTextView.svg?style=flat)](https://cocoapods.org/pods/ZLAutoHeightTextView)
[![License](https://img.shields.io/cocoapods/l/ZLAutoHeightTextView.svg?style=flat)](https://cocoapods.org/pods/ZLAutoHeightTextView)
[![Platform](https://img.shields.io/cocoapods/p/ZLAutoHeightTextView.svg?style=flat)](https://cocoapods.org/pods/ZLAutoHeightTextView)

`ZLAutoHeightTextView` 是一个基于 `UITextView` 的轻量级输入组件，输入内容时会自动调整高度，并内置占位文案能力，适合评论框、聊天输入框、反馈表单等场景。

## 特性

- 根据文本内容自动增高
- 支持 `minHeight` 和 `maxHeight` 高度限制
- 超过最大高度后自动开启内部滚动
- 支持 `placeholder` 和 `placeholderColor`
- 提供 `heightDidChangeBlock` 回调，方便同步外部布局
- 支持 Interface Builder，可直接在 Storyboard / XIB 中配置

## 安装

### CocoaPods

```ruby
pod 'ZLAutoHeightTextView'
```

然后执行：

```bash
pod install
```

## 系统要求

- iOS 10.0+
- Xcode 版本需支持 CocoaPods 工程构建

## 快速开始

### 代码创建

```objc
#import <ZLAutoHeightTextView/ZLAutoHeightTextView.h>

- (void)viewDidLoad {
    [super viewDidLoad];

    ZLAutoHeightTextView *textView = [[ZLAutoHeightTextView alloc] initWithFrame:CGRectMake(20, 100, self.view.bounds.size.width - 40, 50)];
    textView.minHeight = 50;
    textView.maxHeight = 120;
    textView.placeholder = @"请输入内容";
    textView.placeholderColor = [UIColor lightGrayColor];

    __weak typeof(self) weakSelf = self;
    textView.heightDidChangeBlock = ^(CGFloat newHeight) {
        CGRect frame = textView.frame;
        frame.size.height = newHeight;
        textView.frame = frame;
        [weakSelf.view setNeedsLayout];
    };

    [self.view addSubview:textView];
}
```

### Storyboard / XIB 使用

1. 将 `UITextView` 的自定义类设置为 `ZLAutoHeightTextView`
2. 在运行时属性中配置以下字段：
   - `minHeight`
   - `maxHeight`
   - `placeholder`
   - `placeholderColor`

示例工程已经演示了这套配置方式。

## API

```objc
@property (nonatomic, assign) CGFloat maxHeight;
@property (nonatomic, assign) CGFloat minHeight;
@property (nonatomic, copy) void(^heightDidChangeBlock)(CGFloat newHeight);
@property (nonatomic, copy) NSString *placeholder;
@property (nonatomic, strong) UIColor *placeholderColor;
```

### 属性说明

- `minHeight`：最小高度，小于该值时保持最小高度
- `maxHeight`：最大高度，超过后不再继续增高，改为内部滚动
- `heightDidChangeBlock`：高度变化后的回调
- `placeholder`：占位文本
- `placeholderColor`：占位文本颜色

## 示例工程

先进入 `Example` 目录并安装依赖：

```bash
pod install
```

然后打开工程运行示例：

```bash
open ZLAutoHeightTextView.xcworkspace
```

## 使用场景

- 聊天输入框
- 评论输入区域
- 表单中的多行文本输入
- 需要占位提示且高度自适应的文本编辑场景

## 作者

fanpeng, 2551412939@qq.com

## License

`ZLAutoHeightTextView` 基于 MIT 协议开源，详见 `LICENSE`。
