---
title: "C# MVVM 模式入门指南"
date: 2025-11-13
categories:
  - 编程
  - C#
tags:
  - MVVM
  - WPF
  - 设计模式
---

# 什么是 MVVM？

MVVM（Model-View-ViewModel）是一种软件架构设计模式，在 C# 的 WPF、UWP 和 MAUI 等框架中被广泛使用。它能让代码更清晰、更易维护。

## MVVM 的三个核心组件

### 1. Model（模型）
Model 负责处理业务逻辑和数据。它是应用程序的核心，不依赖于界面。

```csharp
public class User
{
    public string Name { get; set; }
    public string Email { get; set; }
    public int Age { get; set; }
}
```

### 2. View（视图）
View 是用户看到的界面，使用 XAML 编写。它只负责显示数据，不包含业务逻辑。

```xml
<TextBlock Text="{Binding UserName}" />
<TextBox Text="{Binding UserEmail}" />
```

### 3. ViewModel（视图模型）
ViewModel 是 View 和 Model 之间的桥梁。它：
- 从 Model 获取数据
- 将数据转换为 View 可以显示的格式
- 处理用户交互逻辑

```csharp
public class UserViewModel : INotifyPropertyChanged
{
    private string _userName;
    public string UserName
    {
        get => _userName;
        set
        {
            _userName = value;
            OnPropertyChanged(nameof(UserName));
        }
    }
    
    // 实现 INotifyPropertyChanged 接口...
}
```

## MVVM 的优势

### 1. 关注点分离
- UI 设计师可以专注于 View
- 开发者可以专注于 ViewModel 和 Model
- 团队协作更高效

### 2. 易于测试
ViewModel 不依赖于 UI，可以轻松进行单元测试。

```csharp
[Test]
public void TestUserNameUpdate()
{
    var viewModel = new UserViewModel();
    viewModel.UserName = "Pogo";
    Assert.AreEqual("Pogo", viewModel.UserName);
}
```

### 3. 代码重用性高
ViewModel 可以被多个 View 复用，同一份逻辑可以用于不同的界面。

## 数据绑定的魔法

MVVM 的核心是**数据绑定**（Data Binding）。当 ViewModel 中的数据变化时，View 会自动更新，反之亦然。

```xml
<!-- View 自动显示 ViewModel 中的数据 -->
<TextBlock Text="{Binding UserName, Mode=TwoWay}" />
```

## 实际应用场景

MVVM 特别适合：
- WPF 桌面应用程序
- UWP Windows 应用
- Xamarin/MAUI 跨平台移动应用
- 需要复杂 UI 交互的项目

## 学习建议

如果你想深入学习 MVVM：

1. **掌握数据绑定基础** - 这是 MVVM 的核心
2. **学习 INotifyPropertyChanged** - 实现属性变化通知
3. **了解 ICommand 接口** - 处理用户命令
4. **使用 MVVM 框架** - 如 Prism、MVVM Light、CommunityToolkit.Mvvm

## 小结

MVVM 模式虽然一开始可能觉得复杂，但它能让大型项目的代码结构更清晰、更易维护。一旦掌握，你会发现它是开发 C# 桌面和移动应用的最佳实践。

从简单的项目开始练习，慢慢就能体会到 MVVM 的强大之处！

---

*你对 MVVM 有什么疑问吗？欢迎在评论区讨论！*
