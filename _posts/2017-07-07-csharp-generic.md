---
layout: single
title: C# 제네릭(Generic) 응용
description: "C# 제네릭(Generic) 응용에 대해."
tags: [c#]
---

**제네릭(Generic)**은 **형식 매개 변수**라고도 불리는데, **형식 매개 변수**를 사용하면 클래스나 메서드를 선언하고 인스턴스화할 때까지 형식 지정을 연기하는 클래스와 메서드를 디자인할 수 있습니다.

<br>

```csharp
using System;
using System.Collections.Generic;

namespace GenericExample
{
    public class GenericList<T>
    {
        // 중첩 클래스
        private class Node
        {
            // 생성자
            public Node(T t)
            {
                next = null;
                data = t;
            }

            private Node next;
            public Node Next
            {
                get { return next; }
                set { next = value; }
            }

            private T data;
            public T Data
            {
                get { return data; }
                set { data = value; }
            }
        }

        // 생성자
        public GenericList()
        {
            head = null;
        }

        private Node head;

        public void AddHead(T t)
        {
            Node n = new Node(t);
            n.Next = head;
            head = n;
        }

        // foreach, in에서 호출
        public IEnumerator<T> GetEnumerator()
        {
            Node current = head;

            while (current != null)
            {
                yield return current.Data;
                current = current.Next;
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            GenericList<int> list = new GenericList<int>();

            for (int x = 0; x < 10; x++)
            {
                list.AddHead(x);
            }

            foreach (int i in list)
            {
                Console.Write(i + " ");
            }
            Console.WriteLine("
Done");
        }
    }
}
```

<br>

출력 결과

```
9 8 7 6 5 4 3 2 1 0
Done
```

**왜 이런 출력 결과가 나올까?**

값을 입력하는 부분을 보자.

```csharp
for (int x = 0; x < 10; x++)
{
    list.AddHead(x);
}
```

> AddHead() 메서드를 통해 값을 입력하고 있다.<br>
> 이름을 보면 알겠지만 값은 위(머리)로 입력(Push)된다.

<br>

다음과 같은 스택(Stack) 모양으로 값이 입력(Push)된다.

![Stack Push](https://i.imgur.com/uh88K7l.png)

<br>

값이 저장된 구조를 보자.

![Stack Node](https://i.imgur.com/nPl0hAp.png)

위와 같은 **재귀(Recursive)** 형태로 값이 저장되는데, **head 안의 n 안의 data**를 [yield](https://docs.microsoft.com/ko-kr/dotnet/csharp/language-reference/keywords/yield)로 반환하고 다음 객체로 **head 안의 n 안의 next**를 head에 대입하는 과정을 계속 반복한다. ~~양파 껍질 까는 것처럼~~

<br>

값을 출력하는 부분을 보자.

```csharp
foreach (int i in list)
{
    Console.Write(i + " ");
}
```

> [foreach, in](https://docs.microsoft.com/ko-kr/dotnet/csharp/language-reference/keywords/foreach-in)을 통해 값을 가져오고(Pop) 있다. list는 Iterator 객체이다.<br>
> 스택(Stack)은 [후입선출(LIFO)](https://ko.wikipedia.org/wiki/%ED%9B%84%EC%9E%85_%EC%84%A0%EC%B6%9C) 구조이므로 **9부터 0으로** 값을 가져오게(Pop) 된다.

여기서는 예시를 `GenericList<int> list = new GenericList<int>();`로 들었지만, `GenericList<string> list = new GenericList<string>();`으로 바꿔도 같은 동작을 하게 된다.

<br>

-----

[Iterator](https://docs.microsoft.com/ko-kr/dotnet/csharp/programming-guide/concepts/iterators): next() 메서드를 통해 값을 반환하는 반복기 객체이다.<br>
[yield](https://docs.microsoft.com/ko-kr/dotnet/csharp/language-reference/keywords/yield): 메서드, 연산자, 또는 이 키워드가 나타나는 get 접근자가 반복기임을 나타냅니다.<br>
