---
title:  "[Codility] Lesson9. Maximum Slice Problem-MaxSliceSum C언어 풀이" 

categories:
  - Codility
tags:
  - [Codility, C]
 
toc: false
toc_sticky: false

date: 2020-08-30
last_modified_at:
---
# 1. 문제
---
길이가 N인 배열 A가 주어졌을 때, **배열의 합이 가장 큰값을 구하는 문제** $0 \leq P \leq Q < N$

<br>

# 2. 정답
## 첫번째 - 100점
>O(N)

{% highlight c linenos %}
int solution(int A[], int N) {
    int slice = A[0], b = A[0];
    
    for(int i = 1; i < N; i++){
        if(slice + A[i] > A[i])
            slice += A[i];
        else
            slice = A[i];
        
        if(b < slice)
            b = slice;
    }
    return b;
}
{% endhighlight %}


<br>

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}