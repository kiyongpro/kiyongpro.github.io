---
title:  "[Codility] Lesson10. Prime And Composite Numbers-MinPerimeterRectangle C언어 풀이" 

categories:
  - Codility
tags:
  - [Codility, C]
 
toc: false
toc_sticky: false

date: 2020-10-20
last_modified_at:
---
# 1. 문제
---
**부피가 N인 직사각형 중에 가장 적은 둘레의 값을 반화하는 문제**

<br>

# 2. 정답
## 첫번째 - 100점
>O(sqrt(N))

{% highlight c linenos %}
#include<math.h>

int solution(int N) {
    int index = (int)sqrt(N);
    
    while(index > 0){
        if(N % index == 0){
            break;
        }
        index--;
    }
    
    return (index + (N / index)) * 2;
}
{% endhighlight %}

부피가 N인 직사각형의 너비와 높이는 N의 약수이다. 약수를 구하는 방법은 N을 1부터 N까자 나누 었을 때, 나머지가 0이 되는 수이다.   

N의 크기가 너무 크면 계산시간이 오래 걸리게 되는데 이를 줄이기 위하여 N의 **제곱근** 까지만 반복하여도 모든 약수를 구할 수 있다.   

직사각형의 가장 작은 둘레를 구하기 위해서는 너비와 높의의 차가 가장 적을 때이다. 그래서 N의 제곱근부터 1까지 수를 줄여가며 약수를 구한뒤 가장 처음으로 구해지는 약수를 직사각형의 한 면으로 지정하여 둘레를 구하였다.

<br>

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}