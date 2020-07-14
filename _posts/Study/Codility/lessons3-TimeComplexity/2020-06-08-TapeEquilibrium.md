---
title:  "[Codility] Lesson3. TimeComplexity-TapeEquilibrium C언어 풀이" 
excerpt: "Codility c언어 문제 풀이 3-3"

categories:
  - Study
tags:
  - [Codility, C]
 
toc: false
toc_sticky: false

date: 2020-06-08
last_modified_at: 2020-06-09
---

# 1. 문제

길이가 N인 배열 A와 정수 P를 주고, 0부터 P-1의 합과 P부터 N까지의 합을 비교하여 가장 적은 차이가 나는 값을 찾는 문제이다. P는 1부터 시작해 N-1까지 차례로 증가한다.
>예시   
A[0] = 3   
A[1] = 1   
A[2] = 2   
A[3] = 4   
A[4] = 3 일 때,   

- P = 1, A[0] - (A[1] + A[2] + A[3] + A[4]) = 3 - 10 = 7   
- P = 2, (A[0] + A[1]) + (A[2] + A[3] + A[4]) = 4 - 9 = 5   
- P = 3, 6 - 7 = 1
- P = 4, 10 - 3 = 7

최소값 인 1을 반환한다.

<br>

# 2. 정답
## 첫번째 - 100점

{% highlight c linenos %}
int solution(int A[], int N) {
    int sumToP = A[0];
    int sumToN = 0;
    for (int i = 1; i < N; i++) {
        sumToN += A[i];
    }

    int min = abs(sumToP - sumToN);

    for (int i = 2; i < N; i++) {
        sumToP += A[i-1];
        sumToN -= A[i-1];
        
        int diff = abs(sumToP - sumToN);
        if (diff < min) {
            min = diff;
        }
    }
    return min;
}
{% endhighlight %}

`A[0]`값(`sumToP`)과 나머지 값의 합(`sumToN`)의 차(`min`)를 기준값으로 잡는다.   
`A[1]`값에 `sumToP`를 더해주고 `sumToN`에서는 빼준 다음 차(`diff`)를 구한다.   
`diff`가 `min`보다 작으면 `min`에 입력한다.

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}