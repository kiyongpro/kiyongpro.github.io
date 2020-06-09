---
title:  "[Codility] Lesson2. Arrays-OddOccurrenceslnArray C언어 풀이" 
excerpt: "Codility c언어 문제 풀이 2-2"

categories:
  - Algorithm
tags:
  - [Algorithm, Codility, C]

toc: false
toc_sticky: false

date: 2020-06-06
last_modified_at:
---
# 1. 문제

배열 A가 있을 때, 같은 값끼리 짝을 지어주고 짝을 이루지 못한 한개의 값을 반환해주면 된다.   
여기서 배열 A의 길이는 **홀수**이다.

<br>

# 2. 풀이

1. 처음에 0번째 배열 값을 기준으로 잡고 1부터 N까지 값과 비교하여 같은 값이 나왔을 때, 그 값을 0으로 바꿔준다. 예를 들어 A[0] == A[i]이 성립 되면 A[i] = 0을 해주면 된다.
1. 위 과정을 N-1번 만큼 반복해 준다. (비교하기 위해서는 2개의 값이 필요하기 때문에 N번까지 반복할 필요가 없다.)
1. 만약 N까지의 값과 같은 값이 나오지 않았다면 기준으로 잡아둔 값을 반환해준다. 

<br>

# 3. 정답
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

- **5Line** - A[i] 와 A[j]의 값을 비교하여 같은 값이 나오면 A[j]의 값을 0으로 바꿔준다.
- **9Line** - A[i] 와 같은 값이 존재 하지 않으므로 A[i]값을 반환해준다.
- **14Line** - N번 앞의 값들이 모두 짝을 이루었을 경우 A[N-1]번째 값을 반환해준다.

잘못된 부분 : 시간 복잡도가 O(N**2)가 나왔다. N의 값이 10만이 넘어가면 `TIMEOUT ERROR`가 발생하였다.

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