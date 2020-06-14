---
title:  "[Codility] Lesson4. Counting Elements-PermCheck C언어 풀이" 
excerpt: "Codility c언어 문제 풀이 4-4"

categories:
  - Algorithm
tags:
  - [Algorithm, Codility, C]

toc: false
toc_sticky: false

date: 2020-06-11
last_modified_at:
---

# 1. 문제
---
배열 A가 1부터 N까지 연속적인 숫자로 이루어져 있는지 확인하는 문제이다.
>예시   
N = 4 일 때,
A[0] = 4   
A[1] = 1   
A[2] = 3   
A[3] = 2   
순차적이므로 1을 반환해야 한다.

>예시2   
N = 3 일 때,
A[0] = 4   
A[1] = 1   
A[2] = 3   
비순차적이지 0을 반환해야 한다.

<br>

# 2. 정답
## 첫번째 - 100점

{% highlight c linenos %}
int solution(int A[], int N) {
    int* arr = (int*)calloc(N, sizeof(int));

    for (int i = 0; i < N; i++) {
        if (A[i] > N || arr[A[i]]) {
            return 0;
        }
        else {
            arr[A[i]] = 1;
        }
    }
    return 1;
}
{% endhighlight %}

`calloc` 함수를 사용해서 N 크기의 배열 `arr`를 선언해 주었다. 이 변수는 배열 A의 숫자의 중복을 확인할 것이다. 숫자 1이 나오면 `arr[0]`값이 1이 되어 `true`를 뜻한다.

```c
if (A[i] > N || arr[A[i]]) {
  return 0;
}
```
배열 A의 숫자가 순차적이 되기 위해선 N보다 큰 숫자가 나오거나 중복된 숫자가 나오면 불가능하게 된다. 그렇게 되면 0값을 반환한다.

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}