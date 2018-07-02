---
layout: single
title: C# 캐스팅 및 형 변환
description: "C# 캐스팅 및 형 변환에 대해."
tags: [c#]
---

#### int 변수 i를 int최댓값으로 초기화하고 타입과 값을 출력합니다.

```csharp
int i = Int32.MaxValue;
Console.WriteLine(i.GetType());  // System.Int32
Console.WriteLine(i);  // 2147483647
```

> 숫자 타입의 클래스에는 최댓값을 가져올 수 있는 속성이 있다.

<br>

#### long 변수 l에 i를 대입하고 타입과 값을 출력합니다.

```csharp
long l = i;  // 암시적 형 변환(Up Casting)
Console.WriteLine(l.GetType());  // System.Int64
Console.WriteLine(l);  // 2147483647
```

> 작은 타입에서 큰 타입에 대입하면 암시적 형 변환이 일어난다.<br>
> long으로 알려진 정수형 타입은 int의 64bit이다.

<br>

```csharp
byte b = (byte)i;  // 명시적 형 변환(Down Casting)
Console.WriteLine(b.GetType());  // System.Byte
Console.WriteLine(b);  // 255
```

> 작은 타입으로 형 변환을 할 때에는 실수가 아님을 명시하기 위해 (type)을 써준다.<br>
> 작은 타입으로 형 변환을 하면 담을 수 있는 크기만큼 값이 제한되어 대입하게 된다.

<br>

#### short 변수 s를 65로 초기화하고 char 변수 c에 대입하고 타입과 값을 출력합니다.

```csharp
short s = 65;
char c = (char)s;  // 명시적 형 변환
Console.WriteLine(c.GetType());  // System.Char
Console.WriteLine(c);  // A
```

> 숫자와 문자라는 전혀 다른 타입에도 형 변환이 가능하다.
