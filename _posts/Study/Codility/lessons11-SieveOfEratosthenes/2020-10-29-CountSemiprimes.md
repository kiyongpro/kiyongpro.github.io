---
title:  "[Codility] Lessons11. SieveOfEratosthenes-CountSemiprimes C언어 풀이" 

categories:
  - Codility
tags:
  - [Codility, C]
 
toc: false
toc_sticky: false

date: 2020-10-29
last_modified_at:
---
# 1. 문제
---
P와 Q사이의 semiprime(약수가 소수 2개로 이루어진 숫자) 개수를 구하는 문제

>prime number

- 2,3,5,7 ...

>semiprime number

- 4(2*2), 6(2*3), 9(3*3), 10(2*5), 14(2*7) ...

<br>

# 2. 정답
## 첫번째 - 100점
> O(N * log(log(N)) + M)

{% highlight c linenos %}
struct Results solution(int N, int P[], int Q[], int M) {
    struct Results result;
    int* prime = (int*)calloc(N/2+1,sizeof(int));
    int* s = (int*)calloc(N+1, sizeof(int));
    
    //prime 구하기
    //소수가 아닌 수에 1을 삽입하여준다. 소수는 0이 된다.
    for(int i = 2; i+i <= N; i++){
        if(prime[i] == 0){
            for(int j = i+i; j+j <= N; j=j+i){
                prime[j] = 1;
            }
        }
    }
    
    //semiprime 구하기
    for(int i = 2; i+i <= N; i++){
        if(prime[i] == 0){
            for(int j = i; i*j <= N; j++){
                if(prime[j] == 0){
                    s[i*j] = 1;
                }
            }
        }
    }

    //semiprime 총 개수 계산
    for(int i = 1; i <= N; i++)
        s[i] += s[i-1];
    
    int* ans = (int*)malloc(sizeof(int) * M);
    
    for(int i = 0; i < M; i++){
        ans[i] = s[Q[i]] - s[P[i]-1];
    }
    
   
    result.A = ans;
    result.M = M;
    return result;
}
{% endhighlight %}

- prime를 구한다. 최소한의 숫자로 2가 들어가야 하므로 N/2개 이상으로 구할 필요는 없다. 
- semiprime은 소수의 곱셈으로 구한다.   

||0|1|2|3|4|5|6|7|8|9|10|11|12|
|semi|0|0|0|0|1|0|1|0|0|1|1|0|0|

- semiprime의 총 갯수를 구한다.

||0|1|2|3|4|5|6|7|8|9|10|11|12|
|semi|0|0|0|0|1|1|2|2|2|3|4|4|4|

- 6 과 12 사이의 semiprime 개수 = > s[12] - s[6-1] => 4 - 1 => 3


<br>

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}