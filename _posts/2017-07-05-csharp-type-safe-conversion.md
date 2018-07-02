---
layout: single
title: C# 안전한 형 변환
description: "C# 안전한 형 변환에 대해."
tags: [c#]
---

#### 클래스 정의

```csharp
class A
{
    int i = 100;
}

class B : A
{
    int j = 200;
}

class C
{
    int x = 500;
}
```

<br>

```csharp
A a1 = new A();
Console.WriteLine(a1 is A);  // True
```

> a1은 A의 인스턴스이다.

<br>

```csharp
B b1 = new B();
Console.WriteLine(b1 is A);  // True
Console.WriteLine(b1 is C);  // False
```

> b1은 A와 상속 관계에 있다.<br>
> b1은 C의 인스턴스도 아니고 상속 관계도 아니다.

<br>

```csharp
object[] strArray = new object[3] { "1", 2, "3" };
string str1 = strArray[0] as string;
Console.WriteLine(str1 != null ? str1 : "null");  // 1
string str2 = strArray[1] as string;
Console.WriteLine(str2 != null ? str2 : "null");  // null
```

> strArray[0]은 str1으로 형 변환 대입이 가능하고 값은 1이다.<br>
> strArray[1]은 str2로 현 변환 대입이 불가능하고 값은 null이다.
