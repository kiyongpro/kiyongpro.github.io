---
title:  "[코딩도장] Multiples of 3 and 5 C#문제풀이" 

categories:
  - Study
tags:
  - [코딩도장, C#, CSharp]
 
toc: false
toc_sticky: false

date: 2020-07-23
last_modified_at:
---

알고리즘 풀이 사이트인 **코디도장**의 문제를 풀이해 보았다. 한국사이트라서 번역을 할 필요가 없으며, 문제가 lv1부터 lv5까지 다섯단계로 분류한 부분이 좋았다. 하지만 따로 컴파일러가 없어 직점 프로그램을 실행하여 나의 문제를 확인 해야 했는데, 이 과정에서 내 풀이가 맞았는가? 최적화가 잘 되었는가?에 대한 피드백이 나오질 않아서 아쉬웠다. 하지만 다른 사람들의 풀이과정을 덧글형식으로 작성하는 방식이라서 나와는 다른 풀이과정이나 다른언어를 사용한 해답을 볼 수 있어서 좋은 공부가 되었다.
{: .notice--warning}

# 1. 문제
> LV.1

10미만의 자연수에서 3과 5의 배수를 구하면 3,5,6,9이다. 이들의 총합은 23이다.   
1000미만의 자연수에서 3,5의 배수의 총합을 구하라.

# 2. 풀이
## 첫번째
{% highlight c linenos %}
int sum = 0;
for(int i = 1; i < 1000; i++)
{
    if (i % 3 == 0 || i % 5 == 0) sum += i;
}
{% endhighlight %}

> 정답 : 233168

1부터 1000까지 반복하면서 3또는 5의 배수가 나오면 sum에 더해주는 형식이다. 가장 간단하고 많은사람이 같은 방식으로 풀이를 하였다.

## 두번째
{% highlight c linenos %}
class Program
{        
    static void Main(string[] args)
    {
        Console.WriteLine(Calc(3, 5, 1000));
    }

    static int Calc(int a, int b, int n)
    {
        return Explan(a, n) + Explan(b, n) - Explan(LCM(a, b), n);
    }
    static int Explan(int num, int n)
    {
        int count = (n - 1) / num;
        return (count * (count + 1) / 2) * num;
    }

    static int LCM(int a, int b)
    {
        return a * b / GCD(a, b);
    }

    static int GCD(int a, int b)
    {
        while (b != 0)
        {
            int temp = a % b;
            a = b;
            b = temp;
        }
        return a;
    }
}
{% endhighlight %}

문제가 너무 정적인 느낌이 들어서 다른 방식으로 풀어보았다. 2개의 숫자와 1개의 범위를 입력하면 계산하는 방식이다.

- 결과값을 반복문 없이 하려고 하였다 범위가 1000이면 999번을 반복 하기 때문에 그 과정을 줄일 수 있을 것 같았다.
- **유클리드 호제법**을 사용하여 최대공약수(GCD)와 최소공배수(LCM)을 구해주었다.

첫번째 = a, 두번째 = b, 범위를 = n이라고 가정할 때,   

result = n까지의 a배수의 합 + n까지의 b배수의 합 - n까지의 LCM(a, b)배수의 합    

n까지의 a배수의 합 = n/a(배수의 갯수)를 최대값으로 가지는 시작값과 등차가 1인 등차수열 * a   
예를 들어 a = 3, n = 1000일 때, n / a = 333, (1 + 2 + 3... + 333)

- 등차수열은 **가우스 덧셈공식**을 사용하여 풀어주었다.   

1부터 n까지의 합 $n * (n + 1) / 2$


[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}