# Dart
**概念**：是谷歌开发的，类型安全的，面向对象的编程语言，被应用于web、服务器、移动应用和物联网等领域。Flutter是基于Dart开发的。生态是 <a href="https://pub.dev">https://pub.dev</a>

# 语法基础
```dart
// 声明函数
void printInteger(int aNumber){
    print('number is $aNumber');
}

// 入口文件 —— 应用从这里开始执行
void main(){
    var number = 42;
    printInteger(number);
}
```

# 变量
**声明变量**：
- 明确指定类型：`int age = 18;`
- 不明确类型：`var age = 18;` 或 `dynamic age = 18;`

**声明常量**：
- `const age = 18;` 无法将运行时的值分配给const变量
- `final age = 18;` 可以将运行时的值分配给const变量

变量名大小写敏感。变量名默认值为null (JS中默认为undefined)。不会进行隐式转换