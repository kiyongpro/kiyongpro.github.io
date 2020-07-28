---
title:  "[코딩도장] Self Number의 합 C#문제풀이" 

categories:
  - Study
tags:
  - [코딩도장, C#]
 
toc: false
toc_sticky: false

date: 2020-07-24
last_modified_at:
---


# 1. 문제
> LV.2

넥슨 입사문제라는 제목으로 작성되었다.   
자연수 $n$이 있을 때, $d(n)$은 $n$의 각 자릿수의 숫자들과 n의 합이라고 정의한다.

>$d(91) = 9 + 1 + 91 = 101$

이 때, n을 d(n)의 제네레이터(generator)라고 한다. 91은 101의 제네레이터라는 뜻이다. 여기서 101은 100또한 제네레이터로 가지고 있다. 반대로 제네레이터를 가지지 못한 숫자도 있는데 이를 셀프넘버(self-number)라고 불린다. 예를 들어 1,3,4,7,9,20,31 은 셀프 넘버이다.

1이상이고 5000 보다 작은 셀프 넘버들의 합을 구하라.

# 2. 풀이

{% highlight cs linenos %}
int result = 4999 * 5000 / 2;

bool[] generated = new bool[5000];

for (int n = 1; n < 5000; n++)
{
    int d = n + (n / 1000) + (n / 100 % 10) + (n / 10 % 10) + (n % 10);

    if (d >= 5000) continue;                
    if (!generated[d])
    {
        result -= d;
        generated[d] = true;
    }
}
{% endhighlight %}

> 정답 : 1227365

- 1부터 4999까지의 합을 미리 result에 입력한 뒤 제네레이터가 존재하는 d(n)의 값을 빼면 남은 값은 self-number의 합이 된다.
- self-number의 값을 구해서 더해주는 방식은 반복문(for)을 2번 사용하기에(값을 구할 때, 값을 더할 때) 위 같은 방법으로 1번만 사용하였다.
- 제네레이터의 값이 달라도 d(n)의 값이 중복될 수 있기에 `bool generated`변수를 사용하여 하나의 값만 적용되게 하였다. (91과 100의 d(n) = 101 이기 때문에 101을 2번 뺄 수 있다.)



[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}