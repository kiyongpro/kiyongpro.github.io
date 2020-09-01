---
title:  "[Codility] Lesson9. Maximum Slice Problem-MaxProfit C언어 풀이" 

categories:
  - Codility
tags:
  - [Codility, C]
 
toc: false
toc_sticky: false

date: 2020-08-29
last_modified_at:
---
# 1. 문제
---
길이가 N인 배열 A가 주어졌을 졌다. **A[P]에 주식을 사서 A[Q]에 팔았을 때, 시세차익이 가장 높을 때를 구하는 문제**  P < Q   
- N : 0 ~ 400,000   
- A range : 0 ~ 200,000

<br>

# 2. 정답
## 첫번째 - 100점
>O(N)

{% highlight c linenos %}
int solution(int A[], int N) {
    int gain = 0, k = 0;
    for(int i = 1; i < N; i++){
        if(gain  < A[i] - A[k])
            gain = A[i] - A[k];
        else if(A[k] > A[i])
            k = i;
    }
    return gain;
}
{% endhighlight %}

<br>

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}