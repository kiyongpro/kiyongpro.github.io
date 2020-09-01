---
title:  "[Codility] Lesson10. Prime And Composite Numbers-CountFactors C언어 풀이" 

categories:
  - Codility
tags:
  - [Codility, C]
 
toc: false
toc_sticky: false

date: 2020-08-31
last_modified_at:
---
# 1. 문제
---
정수 N이 주어졌을 때, **N의 약수의 개수를 구하는 문제**

<br>

# 2. 정답
## 첫번째 - 100점
>O(sqrt(N))

{% highlight c linenos %}
int solution(int N) {
    int count = 0, index = 1;
    double rootN = sqrt(N);
    
    while(index < rootN){
        if(N % index == 0)
            count += 2;
        index++;
    }
    if(index == rootN)
        count++;
        
    return count;
}
{% endhighlight %}

N의 루트 만큼 반복하는 방식이다. N = 24 일 때 제곱근이 4.1... 이다. 약수는 (1,24), (2, 12), (3, 8) (4, 6)으로 8개이다. 앞자리가 N의 제곱근 이상으로 가지 않아도 구할 수 있다.   
예외로 N = 25가 주어졌을 때, 제곱근이 5 이며 (5,5)가 약수로 나온다. 이때는 중복되는 수를 빼주어야한다. 


<br>

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}