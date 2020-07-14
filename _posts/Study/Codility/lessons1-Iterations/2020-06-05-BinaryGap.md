---
title:  "[Codility] Lesson1. Iterations-BinatyGap C언어 풀이" 
excerpt: "Codility c언어 문제 풀이 1-1"

categories:
  - Study
tags:
  - [Codility, C]
 
toc: false
toc_sticky: false

date: 2020-06-05
last_modified_at: 2020-06-09
---
# 개인적인 평가
---
Codility 알고리즘 문제 풀이 사이트의 문제를 풀어보았습니다. Lessons과 Challenges 두가지 메뉴가 있었는데 Lessons은 1~17단계로 보고 공부하기 편하게 나뉘어져 있어서 좋았습니다. Challenges는 숙련자용 시험같은 느낌이 었습니다. 아쉬운점은 한글 번역이 없다는 점이었습니다. 영어도 잘 못하는데 몇몇 문제는 설명이 부실해서 이해하기 어려웠습니다.
<br>

[Codility바로가기](https://app.codility.com/programmers/) 

<br>

# Lesson1 Iterations(반복)
---
  반복이란 같은 일을 되풀이함 이라는 사전적 의미를 지니고 있습니다. 프로그래밍을 대부분의 상황에서는 같은 코딩을 반복해서 사용해야 할 부분이 있습니다. 예를 들어 `"Hello, World!"`라는 문구를 100000번을 반복 출력할 때, `printf("Hello, Wolrd!");`를 100000번 코딩해야 합니다. 어렵고 불가능한 일을 아니지만, 심리적으로 상당히 힘이 드는 부분입니다. 이러한 상황에서 `for`또는 `while`과 같은 프로그래밍 반복문을 사용하게 되면, 시간과 비용면에서 또한 상당한 이익을 챙길 수 있게 될 수 있을 겁니다.

<br>

# 1. 문제
---
양수 N을 2진수로 변환하여 1 사이에 있는 0의 개수를 찾으면 되는 문제이다.    
> 예시   
N = 9(1001) (1사이에 0이 2개이므로 2를 반환해준다.)   
N = 529(1000010001) (답이 2개 이상이면, 더 큰 수인 4를 반환해준다.)   
N = 15(1111), N = 32(100000) (0이 없거나 1이 하나인 경우는 0을 반환해준다.)

<br>

# 2. 정답
## 첫번째 - 100점
{% highlight c linenos %}
int solution(int N) {
    int answer = 0, max = 0, flag = 0;
    while(N>1){
        if(N % 2){
            flag = 1;
            max = 0;
        }else if(flag){
            max++;
            if(answer < max) answer = max;            
        }
        N /= 2;
    }
    return answer;
}
{% endhighlight %}

10진수의 숫자 `N`을 2진수로 변환과 동시에 0 또는 1인지를 파악하여 숫자를 세어주었다.

>예시   
N = 9 일때,

- while(9>1) //참   
9 % 2 = 1 (xxx1)   
`max`값을 0으로 초기화 및 `flag`값은 1이 나왔는지 참(1)과 거짓(0)을 확인하는 변수이다.   

- while(4>1) //참   
4 % 2 = 0 (xx01)      
숫자 1다음에 0이 나왔으므로 카운트를 시작한다.   
max = 1, answer = 1

- while(2>1) //참   
2 % 2 = 0 (x001)   
max = 2, answer = 2

- while(1>1) //거짓 
1 % 2 = 1 (1001)   
answer = 2 값을 반환해준다.

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}