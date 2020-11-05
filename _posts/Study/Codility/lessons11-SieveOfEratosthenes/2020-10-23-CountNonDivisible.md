---
title:  "[Codility] Lessons11. SieveOfEratosthenes-CountNonDivisible C언어 풀이" 

categories:
  - Codility
tags:
  - [Codility, C]
 
toc: false
toc_sticky: false

date: 2020-10-23
last_modified_at:
---
# 1. 문제
---
N개의 크기로 이루어진 배열 A가 주어질 때, 각각 나누어지지 않는 수의 개숫를 반환하는 문제   

> 예시   

- A[0] / A[1] ~ A[N-1] != 0 의 개수 => answer[0]   
- A[1] / A[0], A[2] ~ A[N-1] != 0 의 개수 => answer[1]   
**...**   
- A[N-1] / A[0] ~ A[N-2] != 0 의 개수 => answer[N-1]   
- **answer 반환**


<br>

# 2. 정답
## 첫번째 - 66점
> O(N ** 2)

{% highlight c linenos %}
struct Results solution(int A[], int N) {
    struct Results result;
    int* ans = (int*)malloc(sizeof(int)*N);
    for(int i = 0; i < N; i++){
        int count = 0;
        for(int j = 0; j < N; j++){
            if(i == j)
                continue;
            if(A[i] % A[j])
                count++;
        }
        ans[i] = count;
    }
    result.L = N;
    result.C = ans;
    
    return result;
}
{% endhighlight %}

생각나는대로 반복문 2개를 이용하여 A[0]을 나머지 배열과 나누어 값을 찾고 다음으로 A[1].. A[N-1] 순으로 반복 하였다. 당연하게도 배열이 길어지면 시간이 길어졌다.

<br>

## 두번째 - 100점
> O(N * log(N))

{% highlight c linenos %}
struct Results solution(int A[], int N) {
    struct Results result;
    //배열 A의 숫자를 분류해놓을 배열 ex) 1 : 1개 2: 1개 .. 
    int* num = (int*)calloc(N*2+1, sizeof(int));
    //나누어지는 수가 몇개인지 저장할 배열 ex) mem[3] = 3으로 나누어지는 배열의 숫자
    int* mem = (int*)calloc(N*2+1, sizeof(int));
    int* ans = (int*)malloc(sizeof(int)*N);
    
    //A를 분류
    for(int i = 0; i < N; i++)
        num[A[i]]++;    
    
    for (int i = 1; i <= N*2+1; i++) {
        if(num[i] != 0)
            for (int j = i; j <= N*2+1; j += i) {
                mem[j] += num[i];
            }
    }

    //나누어 지지 않는 숫자
    for(int i = 0; i < N; i++)
        ans[i] = N - mem[A[i]];
    
    result.L = N;
    result.C = ans;
    
    return result;
}
{% endhighlight %}


<br>

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}