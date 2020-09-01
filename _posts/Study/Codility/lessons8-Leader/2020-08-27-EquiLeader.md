---
title:  "[Codility] Lesson8. Leader-EquiLeader C언어 풀이" 

categories:
  - Codility
tags:
  - [Codility, C]
 
toc: false
toc_sticky: false

date: 2020-08-27
last_modified_at:
---
# 1. 문제
---
길이가 N인 배열 A와 정수형 변수 S가 주어졌을 떄, **0 ~ S의 리더와 S+1 ~ N-1의 리더가 동일한지 구하는 문제**   
S값의 범위는 `0 ~ N-2` 이다.

<br>

# 2. 정답
## 첫번째 - 100점
>O(N)

{% highlight c linenos %}
int solution(int A[], int N) {
    int value = 0, sizeR = 0, sizeL = 0, count = 0;
    
    for(int i = 0; i < N; i++){
        if(count == 0 || value == A[i]){
            count++;
            value = A[i];
        }else{
            count--;
        }
    }
    if(count > 0){
        for(int i = 0; i < N; i++){
            if(value == A[i]){
                sizeR++;
            }
        }
    }
    if(sizeR * 2 <= N) return 0;
    
    int result = 0;
    for(int i = 0; i < N-1; i++){
        if(A[i] == value){
            sizeL++;
            sizeR--;
        }
        if(sizeL * 2 > i + 1 && sizeR * 2 > N-i-1)
            result++;
    }
    
    return result;
}
{% endhighlight %}

8-1번 문제 Dominator와 동일하게 배열 A의 리더값을 구해준다. 리더값의 개수가 N/2보다 크지 않다면 결과 값은 0이 나온다.   
위 과정으로 구한 값은 오른쪽(S+1 ~ N-1)의 리더개수`sizeR`이다. 오른쪽 맨처음 값을 왼쪽으로 하나 보내게 되는데 그 값이 리더와 같으면 왼쪽개수를 더하고`sizeL++`, 오른쪽개수를 빼준다.`sizeR--`   
왼쪽과 오른쪽 각각 리더개수와 총 배열 길이를 비교하여 서로 리더개수가 반이상이 되면 값을 더해준다.`result++`

<br>

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}