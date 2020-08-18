---
title:  "[코딩도장] 문자열 압축 C#문제풀이" 

categories:
  - 코딩도장
tags:
  - [코딩도장, C#]
 
toc: false
toc_sticky: false

date: 2020-07-31
last_modified_at:
---


# 1. 문제
> LV.2

문자열을 입력받아서, 같은 문자가 연속적으로 반복되는 경우 반복 횟수 표시하기
>예시
입력: aaabbcccccca

출력: a3b2c6a1

# 2. 풀이

{% highlight cs linenos %}
static void Main()
{
    string input = Console.ReadLine()+'\0';
    string output = null;
    char compare = input[0];
    int count = 0;

    foreach(char n in input)
    {
        if (n != compare)
        {
            output += compare + count.ToString();
            compare = n;
            count = 0;   
        }
        count++;
    }
    Console.WriteLine(output);        
}
{% endhighlight %}

> foreach 표

||0|1|2|3|4|5|6|7|8|9|10|11|12|
|input|a|a|a|b|b|c|c|c|c|c|c|a|null|
|compare|a|a|a|a|b|b|c|c|c|c|c|c|a|
|output||||a3||b2||||||c6|a1|




[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}