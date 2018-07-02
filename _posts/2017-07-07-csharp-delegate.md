---
layout: single
title: C# 대리자(Delegate)
description: "C# 대리자(Delegate)에 대해."
tags: [c#]
---

**대리자** 또는 **델리게이트**라고 불리는 C#의 **Delegate**는 메서드를 **대신 호출**해주는 역할을 합니다.<br>
대리자는 메서드를 다른 메서드에 인수로 전달하는 데 사용됩니다.<br>
대리자가 래핑할 메서드의 이름을 제공하거나 [무명 메서드](https://docs.microsoft.com/ko-kr/dotnet/csharp/programming-guide/statements-expressions-operators/anonymous-methods), [람다 식](https://docs.microsoft.com/ko-kr/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions)을 사용하여 생성합니다.

<br>

## 대리자 사용

아래와 같이 **메서드**를 정의하고

```csharp
// 메서드 정의 (string 입력, void 출력)
public static void DelegateMethod(string message)
{
    System.Console.WriteLine(message);
}
```

<br>

아래와 같이 **대리자 메서드**를 정의합니다.

```csharp
// 대리자 메서드 정의 (string 입력, void 출력)
public delegate void Del(string message);
```

<br>

이렇게 사용할 수 있습니다.

```csharp
// 대리자 초기화
Del handler = DelegateMethod;

// 대리자 호출
handler("Hello World");
```

<br>

흠...

.

.

.

<br>

## 그냥 메서드를 호출하면 되지 않은가?

## → 대리자를 쓰는 곳은 따로 있다.

<br>
<br>
<br>

### 일반적으로 이렇게 쓴다. (콜백)

```csharp
using System;

namespace DelegateExample
{
    public delegate double Del(double a, double b);

    class Program
    {
        public static void Calculator(double a, double b, Del callback)
        {
            Console.WriteLine(callback(a, b));
        }

        public static double Plus(double a, double b) { return a + b; }
        public static double Minus(double a, double b) { return a - b; }
        public static double Multiply(double a, double b) { return a * b; }
        public static double Divide(double a, double b) { return a / b; }

        static void Main(string[] args)
        {
            Del plus = Plus;
            Del minus = Minus;
            Del multiply = Multiply;
            Del divide = Divide;

            Calculator(10, 5, plus);  // 15
            Calculator(10, 5, minus);  // 5
            Calculator(10, 5, multiply);  // 50
            Calculator(10, 5, divide);  // 2
        }
    }
}
```

> callback을 인자로 넣어 메서드가 메서드를 호출하게 만들었다.

<br>

### 이렇게 줄일 수도 있다. (콜백, 무명 메서드)

```csharp
using System;

namespace DelegateExample
{
    public delegate double Del(double a, double b);

    class Program
    {
        public static void Calculator(double a, double b, Del callback)
        {
            Console.WriteLine(callback(a, b));
        }

        static void Main(string[] args)
        {
            Calculator(10, 5, delegate (double a, double b) { return a + b; });  // 15
            Calculator(10, 5, delegate (double a, double b) { return a - b; });  // 5
            Calculator(10, 5, delegate (double a, double b) { return a * b; });  // 50
            Calculator(10, 5, delegate (double a, double b) { return a / b; });  // 2

        }
    }
}
```

> 무명 메서드는 범위를 벗어나게 되면 메모리에서 해제된다. 오버헤드를 줄일 수 있다.

<br>

### 이렇게 줄일 수도 있다. (콜백, 람다 식 ★)

```csharp
using System;

namespace DelegateExample
{
    public delegate double Del(double a, double b);

    class Program
    {
        public static void Calculator(double a, double b, Del callback)
        {
            Console.WriteLine(callback(a, b));
        }

        static void Main(string[] args)
        {
            Calculator(10, 5, (a, b) => a + b);  // 15
            Calculator(10, 5, (a, b) => a - b);  // 5
            Calculator(10, 5, (a, b) => a * b);  // 50
            Calculator(10, 5, (a, b) => a / b);  // 2
        }
    }
}
```

> 람다 식은 범위를 벗어나게 되면 메모리에서 해제된다. 오버헤드를 줄일 수 있다.

<br>

-----

[무명 메서드](https://docs.microsoft.com/ko-kr/dotnet/csharp/programming-guide/statements-expressions-operators/anonymous-methods): C# 2.0에서 도입되었습니다. [익명 함수](https://docs.microsoft.com/ko-kr/dotnet/csharp/programming-guide/statements-expressions-operators/anonymous-functions)라고도 부릅니다.<br>
[람다 식](https://docs.microsoft.com/ko-kr/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions): C# 3.0에서 도입되었습니다. [익명 함수](https://docs.microsoft.com/ko-kr/dotnet/csharp/programming-guide/statements-expressions-operators/anonymous-functions)라고도 부릅니다.<br>
