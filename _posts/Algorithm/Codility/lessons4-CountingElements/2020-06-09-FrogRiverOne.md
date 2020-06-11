---
title:  "[Codility] Lesson4. Counting Elements-FrogRiverOne C언어 풀이" 
excerpt: "Codility c언어 문제 풀이 4-1"

categories:
  - Algorithm
tags:
  - [Algorithm, Codility, C]

toc: false
toc_sticky: false

date: 2020-06-09
last_modified_at:
---
# Lesson4 Counting Elements(요소 계산)
---
배열을 올바르게 사용하기 위해서는 필요한 부분을 정확하게 가져오거나 내보낼 수 있어야 합니다. 예를 들어, 배열 A에 라면 끓이는 재료들이 들어있다고 가정합시다. 우리는 가장 첫 번째로 물을 가져와 끓여야 할 것입니다. 하지만 스프를 먼저 가져오거나 면을 가져오게 되면 제대로 된 라면이 완성되지 않을 수도 있습니다. 

<br>

# 1. 문제
---
개구리가 강을 건너려고 하는데 강 사이에 나뭇잎이 다 이어지는 시간을 반환하는 문제이다.   
 강의 거리(`X`)가 5이고, 나뭇잎이 떨어지는 시간(`A[]`)이 다음과 같을 때,   
> 예시   
A[0] = 1 => 1번째 자리  
  A[1] = 3 => 1,3번째 자리  
  A[2] = 1   
  A[3] = 4 => 1,3,4번째 자리  
  A[4] = 2 => 1,2,3,4번째 자리  
  A[5] = 3   
  A[6] = 5 => 1,2,3,4,5번째 자리 (건너갈 수 있다.)  
  A[7] = 4   

  반환하는 값은 6이다.

<br>

# 2. 정답
## 첫번째 - 100점

{% highlight c linenos %}
int solution(int X, int A[], int N) {
    int* arr = (int*)calloc(X, sizeof(int));
    int result = 0;

    for (int i = 0; i < N; i++) {
        if (!arr[A[i] - 1]) {
            arr[A[i] - 1] = 1;
            result++;
            if (result == X) return i;            
        }
    }
    return -1;
}
{% endhighlight %}

나뭇잎의 유무를 확인할 길이가 `X`인 배열(`arr`)을 `calloc`함수를 사용하여 생성해 주었다. `calloc`은 동적 할당으로 배열을 생성해주며 모든 값을 0으로 초기화 시켜준다.     
배열 A의 값을 확인하여 나뭇잎이 떨어지면 같은 자리의 배열 arr에 1(true)을 입력해고 `result`값을 하나 올려준다.   
`result`와 `X`값이 같게 되면 정답을 출력한다.   
> 예시   
  X = 5 이며, 배열A가 다음과 같을 때,
  A[0] = 1   
  A[1] = 3   
  A[2] = 1   
  A[3] = 4   
  A[4] = 2   
  A[5] = 3   
  A[6] = 5   
  A[7] = 4 

- i = 0   
A[0] = 1, arr[0] = 0 이므로 1을 입력한다. result = 1

- i = 1   
A[1] = 3, arr[2] = 0 이므로 1을 입력한다. result = 2

- i = 2   
A[2] = 1, arr[0] = 1 이므로 다음으로 넘어간다.

- i = 3   
A[3] = 4, arr[3] = 0 이므로 1을 입력한다. result = 3

- i = 4   
A[4] = 2, arr[1] = 0 이므로 1을 입력한다. result = 4

- i = 5   
A[5] = 3, arr[2] = 1 이므로 다음으로 넘어간다.

- i = 6   
A[6] = 5, arr[4] = 0 이므로 1을 입력한다. result = 5   
result == X 가 성립하여 6을 반환한다.

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}