---
title:  "[Codility] Lesson9. Maximum Slice Problem-MaxDoubleSliceSum C언어 풀이" 

categories:
  - Codility
tags:
  - [Codility, C]
 
toc: false
toc_sticky: false

date: 2020-08-28
last_modified_at:
---
# 1. 문제
---
길이가 N인 배열 A가 주어졌을 때, **'x~y', 'y~z' 사이의 합중 가장 큰 값을 반환하는 문제**   
- $0 \leq x<y<z<N$
- N : 3 ~ 100,000
- A range : -10,000 ~ 10,000

<br>

# 2. 정답
## 첫번째 - 100점
>O(N)

{% highlight c linenos %}
int solution(int A[], int N) {
    int* sliceLeft = (int*)calloc(N, sizeof(int));
    int* sliceRight = (int*)calloc(N, sizeof(int));
    
    for(int i = 1; i < N-1; i++){
        if(sliceLeft[i-1] > -A[i])
            sliceLeft[i] =  sliceLeft[i-1] + A[i];
        if(sliceRight[N-i] > -A[N-1-i])
            sliceRight[N-1-i] =  sliceRight[N-i] + A[N-1-i];
    }
    
    int result = 0;
    for(int i = 1; i < N-1; i++) {
        if(sliceLeft[i-1] + sliceRight[i+1] > result)
            result =  sliceLeft[i-1] + sliceRight[i+1];
    }
    return result;
}
{% endhighlight %}

맨 처음 숫자부터 시작해서 하나씩 더해가며 비교하는 방식이다.   

A[1] = 3, A[2] = 10, A[3] = -100 이라고 가정한다면, 'A[1] ~ A[2]'의 합이 '-A[3]' 보다 작으므로 A[3] 이전의 수는 초기화하고 A[4]부터 다시 합을 시작한다.   

`sliceLeft[k]`는 0부터 k까지의 합을 `sliceRight[k]`는 k부터 N-1까지의 합을 가지고 있다.   
[0 < k < N]   

k의 숫자는 y를 뜻하기에 `sliceLeft[k-1]`은 y이전의 최대값이고 `sliceRight[k+1]`은 y이후의 최대값이다.


<br>

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}