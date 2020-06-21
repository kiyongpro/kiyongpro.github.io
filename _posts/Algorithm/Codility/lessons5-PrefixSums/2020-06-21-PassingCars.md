---
title:  "[Codility] Lesson5. Counting Elements-PassingCars
 C언어 풀이" 
excerpt: "Codility c언어 문제 풀이 5-4"

categories:
  - Algorithm
tags:
  - [Algorithm, Codility, C]

toc: false
toc_sticky: false

date: 2020-06-21
last_modified_at:
---
# 1. 문제
---
0과 1로 이루어진 배열 A가 주어진다.
- 0은 동쪽으로 이동하는 차
- 1은 서쪽으로 이동하는 차

차끼리 서로 몇 번 지나치는지를 세는 문제이다.

```
배열 A:
A[0] = 0
A[1] = 1
A[2] = 0
A[3] = 1
A[4] = 1
```
A[0]의 값 `0`을 기준으로 잡았을 때, 밑으로 1의 값을 가진 배열과 지나치게 된다.
1. **A[0] -> A[1], A[3], A[4]**
1. **A[2] -> A[3], A[4]**

여기서 **5**를 반환해 준다. 만약 반환 값이 1,000,000,000(10억)이 넘어가면 **-1**을 반환해 준다.


<br>

# 2. 정답
## 첫번째 - 100점
>시간 복잡도 : O(N)

{% highlight c linenos %}
int solution(int A[], int N) {
    int count = 0;
    int east = 0;
    
    for(int i = 0; i < N; i++){
        if(A[i] == 0){
            east++;
            continue;
        }
        count +=east;
        if(count > 1000000000)
            return -1;
        
    }
    return count;
}
{% endhighlight %}

`1`값을 기준으로 하여 풀어보았다. A[0] 부터 시작하여 0을 만나면 `east++`을 해주고 1을 만나면 `count`값에 `east`값을 더해준다. 


[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}