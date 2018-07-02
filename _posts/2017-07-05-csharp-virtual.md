---
layout: single
title: C# Virtual
description: "C# Virtual에 대해."
tags: [c#]
---

#### 클래스 Shape 정의

```csharp
public class Shape
{
    public const double PI = Math.PI;  // 한 번만 할당
    protected double x, y;  // 상속된 클래스에만 접근 허용

    public Shape()
    {
    }

    public Shape(double x, double y)
    {
        this.x = x;
        this.y = y;
    }

    public virtual double Area()
    {
        return x * y;
    }
}
```

> abstract로 선언한 게 아닌, 일반 클래스.

<br>

#### Shape 클래스를 상속한 Circle 클래스 정의

```csharp
public class Circle : Shape
{
    public Circle(double r) : base(r, 0)  // base는 Shape를 가리킨다.
    {
    }

    public override double Area()
    {
        return PI * x * x;
    }
}
```

> virtual로 선언된 Area()를 override하여 재정의.

<br>

#### Circle을 객체화하고 Area() 출력

```csharp
Circle c = new Circle(3.0);
Console.WriteLine(c.Area());  // 28.2743338823081
```

<br>

#### virtual이 없다면?

```
Error\tCS0506\t'Circle.Area()': cannot override inherited member 'Shape.Area()' because it is not marked virtual, abstract, or override
```

> Shape.Area()가 virtual, abstract, override로 선언되지 않았기 때문에 위와 같은 오류가 뜨고 컴파일이 안 된다.

<br>

#### override 하지 않는다면?

> 부모 클래스의 Shape.Area()를 호출하게 된다.
