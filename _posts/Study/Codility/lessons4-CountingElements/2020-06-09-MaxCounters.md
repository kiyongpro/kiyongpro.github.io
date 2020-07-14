---
title:  "[Codility] Lesson4. Counting Elements-MaxCounters C언어 풀이" 
excerpt: "Codility c언어 문제 풀이 4-2"

categories:
  - Study
tags:
  - [Codility, C]
 
toc: false
toc_sticky: false

date: 2020-06-09
last_modified_at:
---

# 1. 문제
---
M길이의 배열 A가 주어지진다. 배열 A의 값은 1 ~ (N+1)의 수가 랜덤으로 입력되어있다. 
>예시   
N = 5, M = 7, A 
A[0] = 3   
A[1] = 4   
A[2] = 4   
A[3] = 6   
A[4] = 1   
A[5] = 4   
A[6] = 4 가 다음과 같다고 가정한다.

- A[0] = 3 일 때, (0, 0, 1, 0, 0)
- A[1] = 4 일 때, (0, 0, 1, 1, 0)
- A[2] = 4 일 때, (0, 0, 1, 2, 0)
- A[3] = 6 일 때, (2, 2, 2, 2, 2) (N의 값보다 클 경우 가장 큰 값으로 바꿔준다.)
- A[4] = 1 일 때, (3, 2, 2, 2, 2)
- A[5] = 4 일 때, (3, 2, 2, 3, 2)
- A[6] = 4 일 때, (3, 2, 2, 4, 2) 

(3, 2, 2, 4, 2)값을 반환해준다.

<br>

# 2. 정답
## 첫번째 - 100점

{% highlight c linenos %}
struct Results solution(int N, int A[], int M) {
    struct Results result;
    int maxP = 0, maxL = 0;
    int* answer = (int*)calloc(N, sizeof(int));
    
    for(int i = 0; i < M; i++){
        if(A[i] > N){
            maxL = maxP;
            continue;
        }
        if(answer[A[i]-1] < maxL){
            answer[A[i]-1] = maxL;
        }
        
        answer[A[i]-1]++;
        
        if(answer[A[i]-1] > maxP){
            maxP++;
        }
    }
    
    for(int i =0; i < N; i++){
        if(answer[i] < maxL)
            answer[i] = maxL;
    }
    result.C = answer;
    result.L = N;
    return result;
}
{% endhighlight %}

N보다 큰 수가 나올 때마다 `answer`의 숫자를 대입하기 위해서는 이중반복문을 사용해야해서 O(N<sup>2</sup>)의 시간이 걸릴 수 있다. 그래서 `max`값을 정해두고 마지막에 갱신하기로 하였다.

N = 5라고 가정할 때, 6이나오기 전까지 차례대로 계산을 해준다. `maxP`값을 정해준다.
```c
answer[A[i]-1]++;

if(answer[A[i]-1] > maxP){
  maxP++;
}
```

배열의 값이 6이 나오면 `maxL`에 `maxP`값을 입력해준다.
```c
if(A[i] > N){
  maxL = maxP;
}
```

`answer`의 값이 `maxL`값보다 낮으면 `maxL`값을 입력해준다.
``` c
if(answer[A[i]-1] < maxL){
  answer[A[i]-1] = maxL;
}
```

미리 정해둔 `maxL`값을 입력해준다.
```c
for(int i =0; i < N; i++){
  if(answer[i] < maxL)
      answer[i] = maxL;
}
```

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}