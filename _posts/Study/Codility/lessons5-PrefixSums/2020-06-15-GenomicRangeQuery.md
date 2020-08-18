---
title:  "[Codility] Lesson5. PrefixSums-GenomicRangeQuery C언어 풀이" 
excerpt: "Codility c언어 문제 풀이 5-2"

categories:
  - Codility
tags:
  - [Codility, C]
 
toc: false
toc_sticky: false

date: 2020-06-15
last_modified_at:
---
# 1. 문제
---
문자 A, C, G, T 가 있고 각각 1, 2, 3, 4 라고 한다.
> A == 1   
C == 2   
G == 3   
T == 4   

문자열 S와 길이가 M인 P, Q 배열이 주어진다.
>예시   
S = CAGCCTA, M = 3일 때,   
1. P[0] = 2, Q[0] = 4   
2. P[1] = 5, Q[1] = 5   
3. P[2] = 0, Q[2] = 6

1. **S[2] ~ S[4] = CA<span style ="color:red">GCC</span>TA 답은 C = 2**
2. **S[5] ~ S[5] = CAGCC<span style ="color:red">T</span>A 답은 T = 5**    
3. **S[0] ~ S[6] = <span style ="color:red">CAGCCTA</span> 답은 A = 1**   

답은 [2, 5, 1]반환해야 한다.

<br>

# 2. 정답
## 첫번째 - 62점
>시간 복잡도 : O(N*M)

{% highlight c linenos %}
struct Results solution(char *S, int P[], int Q[], int M) {
    struct Results result;
    int *arr = (int*)malloc(sizeof(int)*M);
    int min = 5;
    for(int i = 0; i<M;i++){
        for(int j =P[i]; j<=Q[i]; j++){
            if(S[j] == 'A'){
                min = 1;
                break;
            }
            if(S[j] == 'C' || min==2){
                min = 2;
                continue;
            }
            if(S[j] == 'G' || min==3){
                min = 3;
                continue;
            }
            min = 4;
        }
        arr[i] = min;
        min = 5;
    }
    result.A = arr;
    result.M = M;
    return result;
}
{% endhighlight %}
이중 반복문은 당연히 통과가 안 될걸 알았지만 생각나는 방법이 없어서 코딩해보았다.

>예시   
S = CAGCCTA, M = 3일 때,   
1. P[0] = 2, Q[0] = 4   
2. P[1] = 5, Q[1] = 5   
3. P[2] = 0, Q[2] = 6

- i = 0 일 때, j = 2 ~ 4
    - j = 2, S[2] = G 이므로 min = 3 이 된다.
    - j = 3, S[3] = C 이므로 min = 2 이 된다.
    - j = 4, S[4] = C 이므로 min = 2 이 된다.
    - min = 2 이다.

- i = 1 일 때, j = 5 ~ 5
    - j = 5, S[5] = T 이므로 min = 5 이 된다.
    - min = 5 이다.

- i = 2 일 때, j = 0 ~ 6
    - j = 0, S[0] = C 이므로 min = 2 이 된다.
    - j = 1, S[1] = A 이므로 min = 1 이 된다.
    - min = 1 이다.

위의 방식대로 흘러가는 코딩을 했다. 역시 이중 반복문으로 인해 처리해야 할 데이터의 수가 많아지면 `TIMEOUT ERROR`가 발생하였다.

## 두번째 - 100점(다른사람 풀이)
>시간 복잡도 : O(N+*M)

{% highlight c linenos %}
struct Results solution(char *S, int P[], int Q[], int M) {
    struct Results result;
    int A[strlen(S)+1];
    int C[strlen(S)+1];
    int G[strlen(S)+1];
    int* arr = (int*)malloc(sizeof(int) * M);
    
    A[0]=C[0]=G[0]=0;
    for(int i = 1; i < strlen(S)+1; i++){
        if(S[i-1] == 'A'){
            A[i]=A[i-1]+1;
            C[i]=C[i-1];
            G[i]=G[i-1];
        }
        else if(S[i-1] == 'C'){
            A[i]=A[i-1];
            C[i]=C[i-1]+1;
            G[i]=G[i-1];
        }
        else if(S[i-1] == 'G'){
            A[i]=A[i-1];
            C[i]=C[i-1];
            G[i]=G[i-1]+1;
        }
        else{
            A[i]=A[i-1];
            C[i]=C[i-1];
            G[i]=G[i-1];
        }
    }
    
    for(int i = 0; i < M; i++){
        if(P[i] == Q[i]){
            if(S[P[i]]=='A')
                arr[i] = 1;
            else if(S[P[i]]=='C')
                arr[i] = 2;
            else if(S[P[i]]=='G')
                arr[i] = 3;
            else
                arr[i] = 4;
        }
        else if(A[P[i]] != A[Q[i]+1])
            arr[i] = 1;
        else if(C[P[i]] != C[Q[i]+1])
            arr[i] = 2;
        else if(G[P[i]] != G[Q[i]+1])
            arr[i] = 3;
        else
            arr[i] = 4;
    }
    result.A = arr;
    result.M = M;
    return result;
}
{% endhighlight %}

다른 방법은 생각나는게 없어서 구글검색의 힘을 빌렸다. 검색을 하다보니 반복문 2번으로 끝내는 코딩을 찾게 되었다.

>첫번째 for   

첫번째 반복문은 A, C, G 각각의 배열을 S+1 크기의 길이만큼 선언해준 후 문자의 증가값을 미리 계산하는 부분이다. 
>예시   
S = CAGCCTA 일 때,

- i = 1   
S[1] = C 이므로 C배열을 더해준다.   
A [0, 0]   
C [0, 1]   
G [0, 0]   

- i = 2   
S[2] = A 이므로 A배열을 더해준다.   
A [0, 0, 1]   
C [0, 1, 1]   
G [0, 0, 0]   
이 뒤로 마지막 문자열 까지 반복해준다.   

- i = 3   
A [0, 0, 1, 1]   
C [0, 1, 1, 1]   
G [0, 0, 0, 1]   

- i = 8   
**A [0, 0, 1, 1, 1, 1, 1, 2]**   
**C [0, 1, 1, 1, 2, 3, 3, 3]**   
**G [0, 0, 0, 1, 1, 1, 1, 1]**   
최종 결과 값이 된다.

>두번째 for

>예시     
1. P[0] = 2, Q[0] = 4   
2. P[1] = 5, Q[1] = 5   
3. P[2] = 0, Q[2] = 6

1. A[2] 와 A[5]의 값을 비교해 본다.   
**A[2] = 1, A[5] = 1** (값이 같다면 S[2] 와 S[4] 사이에는 A가 한번도 나오지 않았다는 이야기가 된다.)   
**C[2] = 1, C[5] = 2** (값이 다르다면 C가 한번이상 나왔다는 뜻이 된다. 여기서 최솟값은 `C = 2`가 된다.)

2. P[1] 와 Q[1]의 값이 같으므로 하나의 문자가 나오게 된다. 그 값이 최솟값이 된다.   
여기서는 `T = 5`가 된다.

3. A[0] 와 A[7]의 값을 비교해 본다.   
**A[0] = 0, A[7] = 2**   
최솟값은 `A = 1`이 된다. 최종값은 **[2, 5, 1]**이 된다.


[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}