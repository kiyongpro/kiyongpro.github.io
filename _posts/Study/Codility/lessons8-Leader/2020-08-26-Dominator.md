---
title:  "[Codility] Lesson8. Leader-Dominator C언어 풀이" 

categories:
  - Codility
tags:
  - [Codility, C]
 
toc: false
toc_sticky: false

date: 2020-08-26
last_modified_at:
---
# Lessons8 Leader(리더)
---
이번 회차의 주제는 리더이다. N길이 배열이 주어졌을 때, 똑같은 값을 가장 많이 가지고 있는 원소가 리더가 된다. 다수결과 같다고 보면 될 것 같다.

# 1. 문제
---
길이가 N인 배열 A가 주어졌을 때, **같은 값이 N/2개 보다 많은 원소의 위치를 찾는 문제**

<br>

# 2. 정답
## 첫번째 - 100점
>O(N*log(N)) or O(N)

{% highlight c linenos %}
int solution(int A[], int N) {
    int value, leader, size = 0, count = 0;
    
    for(int i = 0; i < N; i++){
        if(size == 0 || value == A[i]){
            size++;
            leader = i;
            value = A[i];
        }else{
            size--;
        }
    }
    if(size > 0){
        for(int i = 0; i < N; i++){
            if(value == A[i]){
                if(++count * 2 > N) return leader;
            }
        }
    }
    return -1;
}
{% endhighlight %}

처음에 같은 값이 가장 많은 원소를 구하고, 그 값을 가진 원소의 개수를 파악해서 N/2개보다 많으면 그 `leader`를 반환하고 아니면 `-1`을 반환한다.

<br>

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}