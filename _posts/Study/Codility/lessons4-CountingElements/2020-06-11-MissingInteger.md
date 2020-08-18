---
title:  "[Codility] Lesson4. Counting Elements-MissingInteger C언어 풀이" 
excerpt: "Codility c언어 문제 풀이 4-3"

categories:
  - Codility
tags:
  - [Codility, C]
 
toc: false
toc_sticky: false

date: 2020-06-11
last_modified_at:
---

# 1. 문제
---
배열 A에 포함되어있지 않은 가장 작은 양의 정수를 찾는 문제이다.
>예시   
A = [1, 3, 6, 4, 1, 2] 숫자 5를 반환한다.   
A = [-1, -3] 숫자 1을 반환한다.

<br>

# 2. 정답
## 첫번째 - 100점

{% highlight c linenos %}
int solution(int A[], int N) {
    int* arr = (int*)calloc(N,sizeof(int));
    for (int i = 0; i < N; i++) {
        if (A[i] > 0 && A[i] <= N) {
            arr[A[i] - 1] = 1;
        }
    }
    for (int i = 0; i < N; i++) {
        if (!arr[i])
            return i + 1;
    }
    return N + 1;
}
{% endhighlight %}

`calloc` 함수를 사용해서 N 크기의 배열 `arr`를 선언해 주었다. 이 변수는 배열 A의 숫자의 유무를 확인할 것이다. 숫자 1이 나오면 `arr[0]`값이 1이 되어 `true`를 뜻한다.

A의 값이 0이하인 음수이거나 N을 초과하는 숫자일 경우는 값을 처리하지 않고 넘어갔다. 반환값은 제일 클경우 N+1일 경우이기 때문에 그 이상의 수는 계산할 필요가 없다.

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}