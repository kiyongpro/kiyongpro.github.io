---
title:  "[코딩도장] 1부터 1000까지 각 숫자의 합 C#문제풀이" 

categories:
  - Study
tags:
  - [코딩도장, C#, CSharp]
 
toc: false
toc_sticky: false

date: 2020-07-27
last_modified_at:
---


# 1. 문제
> LV.1

1부터 1000까지 각 숫자의 합을 구하는 문제이다.

>10 ~ 15   
10 = 1, 0   
11 = 1, 1   
12 = 1, 2   
13 = 1, 3   
14 = 1, 4   
15 = 1, 5   

답은 0:1개, 1:7개, 2:1개, 3:1개, 4:1개, 5:1개

# 2. 풀이

{% highlight cs linenos %}
int[] count = new int[10];
for (int i = 1; i <= 1000; i++)
{
    int temp = i;
    while (temp > 0) {
        count[temp % 10]++;
        temp /= 10;
    }
}
{% endhighlight %}

> 정답    
0: 192개
1: 301개
2: 300개
3: 300개
4: 300개
5: 300개
6: 300개
7: 300개
8: 300개
9: 300개

- 0부터 9까지 숫자를 세는 배열을 생성해준다.
- 입력된 숫자(temp)의 1의 자리 숫자를 하나 더해준뒤 10으로 나누어 없애줍니다.   
temp = 134, count[4]++   
temp = 13, count[3]++   
temp = 1, count[1]++   



[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}