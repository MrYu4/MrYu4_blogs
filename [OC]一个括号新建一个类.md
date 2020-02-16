##[OC]一个括号新建一个类

###特别说明

以下代码仅仅用于说明用途，命名也不是特别规范，小朋友不要模仿哦。

###前言

在iOS开发中，我们会经常用到这么一段代码：

```
UIView *myView = [UIView new];
myView.backgroundColor = [UIColor blackColor];
myView.layer.borderWidth = 2.f;
myView.layer.borderColor = [UIColor redColor].CGColor;
[self addSubview:myView];
```

这么看起来貌似没什么问题，实际上也可以编译运行,但是随着不断地编写代码，我们会写出这些代码：

```
UIView *myView1 = [UIView new];
myView1.backgroundColor = [UIColor blackColor];
myView1.layer.borderWidth = 12.f;
myView1.layer.borderColor = [UIColor whiteColor].CGColor;
[self addSubview:myView1];
UIView *myView2 = [UIView new];
myView2.backgroundColor = [UIColor blackColor];
myView2.layer.borderWidth = 7.f;
myView2.layer.borderColor = [UIColor redColor].CGColor;
[self addSubview:myView2];
UIView *myView3 = [UIView new];
myView3.backgroundColor = [UIColor yellowColor];
myView3.layer.borderWidth = 3.f;
myView3.layer.borderColor = [UIColor blueColor].CGColor;
[self addSubview:myView3];
```

所以这个时候我们会看到我们的代码编程一坨一坨的样子，非常难看，这个时候就需要一个小小的办法提升一下代码的可读性。这个方法实际上最早来源于[GCC](https://gcc.gnu.org/onlinedocs/gcc/Statement-Exprs.html)，并被继承到clang中来。

###Statements and Declarations in Expressions

我们进行赋值操作的时候一般是这么操作的：

```
CGFloat t1 = 1.2;
CGFloat t2 = 3.1;
CGFloat a = t1 + t2;
```

实际上我们还能这么操作:

```
CGFloat a = ({
    CGFloat t1 = 1.2;
    CGFloat t2 = 3.1;
    CGFloat result = t1 + t2;
    result;
});
```

实际上就是以小括号内嵌花括号，花括号中可以用写多行代码，最后一句则是你要返回的结果。
最后我们再安排一下最开始的那一大坨代码。

```
UIView *myView1 = ({
    UIView *view = [UIView new];
    view.backgroundColor = [UIColor blackColor];
    view.layer.borderWidth = 12.f;
    view.layer.borderColor = [UIColor whiteColor].CGColor;
    view;
});
[self addSubview:myView1];
UIView *myView2 = [UIView new];
myView2.layer.borderWidth = 7.f;
myView2.layer.borderColor = ({
    UIView *view = [UIView new];
    view.backgroundColor = [UIColor blackColor];
    view.layer.borderWidth = 7.f;
    view.layer.borderColor = [UIColor redColor].CGColor;
    view;
});
[self addSubview:myView2];
UIView *myView3 = ({
    UIView *view = [UIView new];
    view.backgroundColor = [UIColor yellowColor];
    view.layer.borderWidth = 3.f;
    view.layer.borderColor = [UIColor blueColor].CGColor;
    view;
});
[self addSubview:myView3];
```

嗯,就这样吧。

##求打赏
![支付合并.jpg](https://upload-images.jianshu.io/upload_images/13021244-bf118185dafa4e39.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
