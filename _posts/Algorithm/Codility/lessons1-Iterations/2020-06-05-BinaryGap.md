---
title:  "[Codility] Lesson1. Iterations-BinatyGap C언어 풀이" 
excerpt: "Codility c언어 문제 풀이 1-1"

categories:
  - Algorithm
tags:
  - [Algorithm, Codility, C]
 
toc: false
toc_sticky: false

date: 2020-06-05
last_modified_at: 2020-06-06
---
Codility 알고리즘 문제 풀이 사이트의 문제를 풀어보았습니다. 아쉽게도 한글 번역은 되어있지 않아서 문제 해석에 불편함이 있을 수 있습니다.
<br>

[Codility바로가기](https://app.codility.com/programmers/) 

---
Codility 첫 번째 Lesson의 이름은 Iterations(반복)입니다. 반복이란 같은 일을 되풀이함 이라는 사전적 의미를 지니고 있습니다. 프로그래밍을 대부분의 상황에서는 같은 코딩을 반복해서 사용해야 할 부분이 있습니다. 예를 들어 `"Hello, World!"`라는 문구를 100000번을 반복 출력할 때, `printf("Hello, Wolrd!");`를 100000번 코딩해야 합니다. 어렵고 불가능한 일을 아니지만, 심리적으로 상당히 힘이 드는 부분입니다. 이러한 상황에서 `for`또는 `while`과 같은 프로그래밍 반복문을 사용하게 되면, 시간과 비용면에서 또한 상당한 이익을 챙길 수 있게 될 수 있을 겁니다.

---
<br>

# 1. 문제

양수 N을 2진수로 변환하여 1 사이에 있는 0의 개수를 찾으면 되는 문제이다.  
예를 들어, 9(1001)일 때, 답은 **2**이다. 529(1000010001)일 때, 답은 4와 3중 큰 수인 **4**이다.   
15(1111)와 32(100000) 같은 숫자는 **0**을 반환해야 한다.

<br>

# 2.풀이

1. 양수 N을 1이 될 때까지 나누었을때, 나머지 값이 2진수 표기가 된다.   
예를 들어, 정수 13를 2진수 표기 하고 자 할때,   
>13 / 2 = 6 나머지 1  
>6 / 2 = 3 나머지 0  
>3 / 2 = 1 나머지 1   

13의 2진수 표기법은 1101이 된다.

<br>

# 3.정답
## 첫번째 - 100점
{% highlight c linenos %}
int solution(int N) {
    int answer = 0, max = 0, flag = 0;
    int remainder;
    while(N>1){
        remainder = N % 2;
        if(remainder){
            flag++;
            max = 0;
        }else if(flag > 0 && remainder == 0) {
            max++;
            if(answer < max){
                answer = max;
            }
        }
        N = N / 2;
    }
    return flag > 0 ? answer : 0;
}
{% endhighlight %}

- **4Line** - N이 1이 될 때까지 반복하는 반복문이다.
- **6Line** - 나머지가 1이 나왔을 때, `flag++`해준다. `flag`값이 0이라면 1이 한 번도 안 나왔기 때문이다.
- **9Line** - 나머지가 0이 나오고 1이 한 번이라도 나왔을 때, 0의 개수 최댓값을 계산하는 부분이다.
- **17Line** - 삼항연산자를 사용하여 1이 한 번도 안 나왔으면 0을, 아니면 `answer`를 반환한다.

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}