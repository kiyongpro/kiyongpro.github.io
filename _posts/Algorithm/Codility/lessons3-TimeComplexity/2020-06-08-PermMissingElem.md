---
title:  "[Codility] Lesson3. TimeComplexity-PermMissingElem C언어 풀이" 
excerpt: "Codility c언어 문제 풀이 3-2"

categories:
  - Algorithm
tags:
  - [Algorithm, Codility, C]

toc: false
toc_sticky: false

date: 2020-06-08
last_modified_at: 2020-06-09
---

# 1. 문제
---
크기가 N인 배열 A가 주어진다. 배열 A에는 1부터 N+1까지의 숫자가 중복되지 않게 입력되는데 중간에 비어있는 숫자를 찾는 것이다.
>예시   
A[0] = 2   
A[1] = 3   
A[2] = 1   
A[3] = 5

가 주어지면 4를 반환해준다.

<br>

# 2. 정답
## 첫번째 - 80점

{% highlight c linenos %}
int solution(int A[], int N) {
    int result = 0;

    for (int i = 0; i < N; i++) {
        result += A[i];
    }
    return (N + 2) * (N + 1) / 2 - result;
}
{% endhighlight %}

배열 A의 모든 값을 더해주었다.
```c
for (int i = 0; i < N; i++) {   
  result += A[i];   
}
```

그 다음 가우스 공식을 사용하여 1부터 N+1까지의 합을 구한다.
>가우스 공식   
1+2+3+...+(N-2)+(N-1)+N 의 합   
(N+1) * N / 2

두 수의 차를 반환해준다.

잘못된 부분 : N의 크기가 70,000이 넘어가면 `int`형의 범위를 넘어가서 쓰레기 값이 반환된다. `unsigned`을 사용해도 N의 값이 100,000일 경우 50억이 넘어가게 되어 쓰레기 값이 반환된다.

## 두번째 - 100점

{% highlight c linenos %}
int solution(int A[], int N) {
    int result = N+1;

    for (int i = 0; i < N; i++) {
        result += i+1;
        result -= A[i];
    }
    return result;
}
{% endhighlight %}

기본 원리는 같지만, 방식을 달리해 주었다. 1부터 N+1까지 차례로 더해주면서 배열 A 값도 차례로 빼주며`int`형 범위를 넘어가지 않게 바꿔주었다. 

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}