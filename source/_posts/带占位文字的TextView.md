---
title: 带占位文字的TextView
date: 2017-12-16 18:10:23
tags:
		- iOS
---

作为输入框`UITextField`和`UITextView`各有优缺点，开发中经常需要使用到这两个输入框，`UITextField`可以通过`placeholder`这个属性来加入占位文字，但不能换行；`UITextView`虽然能自动换行，却没有placeholder这种方便的方式添加占位文字，虽然可以通过`attributeString`来设置，但还是觉得不是特别方便。
  最好的方法就是自定义一个`UITextView`的子类[PlaceholderView](https://github.com/charlsPrince/PlaceholderView)，那么这个类里面的任何内容都是你说了算，为`UITextView`添加`placeholder`功能只需要简单的两个步骤：一个通知和一个重写`drawRect`方法。
  
<!-- more -->
  
>在初始化时添加通知

```
- (instancetype)initWithFrame:(CGRect)frame textContainer:(NSTextContainer *)textContainer {

    self = [super initWithFrame:frame textContainer:textContainer];
    if (self) {
        [self registerNotification];
    }
    return self;
}

- (void)registerNotification {
    [self unregisterNotification];
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(textDidChange) name:UITextViewTextDidChangeNotification object:nil];

}

```
>通知方法里面告诉`UITextView`需要重绘

```
- (void)textDidChange {
    [self setNeedsDisplay];
}
```
>重绘视图

```
- (void)drawRect:(CGRect)rect {
    if ([self hasText]) {
        return;
    }

    // 设置字体属性

    NSMutableDictionary *attrs = [NSMutableDictionary dictionaryWithCapacity:0];

    attrs[NSFontAttributeName] = self.font;

    attrs[NSForegroundColorAttributeName] = self.placeholderColor;

    rect.origin.x = 5;
    rect.origin.y = 7;
    rect.size.width -= 2 * rect.origin.x;
    rect.size.height -= 2 * rect.origin.y;
    [self.placeholder drawInRect:rect withAttributes:attrs];
}

```


