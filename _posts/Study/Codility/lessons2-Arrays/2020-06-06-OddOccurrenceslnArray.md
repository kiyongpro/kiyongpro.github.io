---
title:  "[Codility] Lesson2. Arrays-OddOccurrenceslnArray C언어 풀이" 
excerpt: "Codility c언어 문제 풀이 2-2"

categories:
  - Codility
tags:
  - [Codility, C]
 
toc: false
toc_sticky: false

date: 2020-06-06
last_modified_at: 2020-06-09
---
# 1. 문제
---
배열 A가 있을 때, 같은 값끼리 짝을 지어주고 짝을 이루지 못한 한개의 값을 반환해주면 되는 문제이다. 여기서 배열 A의 길이는 **홀수**이다.
>예시   
A[0] = 9 A[1] = 3 A[2] = 9   
A[3] = 3 A[4] = 9 A[5] = 7   
A[6] = 9 라고 할때,  

- 9값을 가진 0, 2를 짝지어준다.   
- 3값을 가진 1, 3을 짝지어준다.   
- 9값을 가진 4, 6을 짝지어준다.   
- 짝을 가지지 못한 5의 7 값을 반환해준다.

<br>

# 2. 정답
## 첫번째 - 66점
{% highlight c linenos %}
int solution(int A[], int N) {
    for (int i = 0; i < N-1; i++) {
        if (A[i]) {
            for (int j = i + 1; j < N; j++) {
                if (A[i] == A[j]) {
                    A[j] = 0;
                    break;
                }
                else if (j == N - 1) 
                    return A[i];                
            }
        }
    }
    return A[N - 1];
}
{% endhighlight %}

먼저 `A[0]`를 기준으로 잡고 `A[1] ~ A[N]`중 같은 값을 가지고 있는 배열을 찾아주고, 0 값을 입력하여 다음 탐색에서 제외하도록 하였다. 이 과정을 `A[0] ~ A[N-1]`까지 반복하며 중복되는 값이 없을 때, 그 순번의 배열을 반환해 주었다. 

잘못된 부분 : 반복문을 이중으로 사용하여 시간 복잡도가 O(N<sup>2</sup>)가 나왔다. N의 값이 10만이 넘어가면 `TIMEOUT ERROR`가 발생하였다.

<br>

## 두번째 - 100점(다른사람 풀이) 
{% highlight c linenos %}
int solution(int A[], int N) {
    for(i = 0; i < N; i++)
        result ^= A[i];     
    return result;
}
{% endhighlight %}

역량이 부족해서 구글 검색을 통하여 다른 사람들의 풀이 과정을 살펴보았다. 비트 연산자를 활용하여 반복문 하나로 간단하게 풀어버렸다.   
`^`기호는 `xor`비트 연산자이다. 같은 값이 나오면 0을 아니면 1을 반환한다. 배열의 모든 값을 계산하게 되면 결국에는 중복되지 않는 한 숫자만 나오게 된다.
 
[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}