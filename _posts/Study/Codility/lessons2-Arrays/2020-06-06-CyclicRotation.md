---
title:  "[Codility] Lesson2. Arrays-CyclicRotation C언어 풀이" 
excerpt: "Codility c언어 문제 풀이 2-1"

categories:
  - Codility
tags:
  - [Codility, C] 

toc: false
toc_sticky: false

date: 2020-06-06
last_modified_at: 2020-06-09
---
# Lesson1 Arrays(배열)
---
 배열은 많은 항목을 한 곳에 저장하는 데 사용할 수 있는 데이터 구조입니다.   
 예를 들어, 학생 100명의 수학 점수를 입력받아야 한다고 합시다. 수를 입력받기 위해서는 `int`형 100개를 선언할 필요가 있습니다. 배열을 사용한다면 한 번에 선언으로 100개의 데이터를 관리 할 수 있게 된다는 편리한 장점이 있습니다.

<br>

# 1. 문제
---
정수 N으로 구성된 배열 A를 K값 만큼 회전 시켜주면 되는 문제이다.   
>예시   
A = [3,8,9,7,6], K = 3 일 때,   
[9,7,6,3,8] 값을 반환해준다.

<br>

# 2. 정답
## 첫번째 - 87점
{% highlight c linenos %}
struct Results solution(int A[], int N, int K) {
    struct Results result;
    int cycle = K % N;
    int* answer = (int*)malloc(sizeof(int) * N);    

    if (cycle == 0) {
        result.A = A;
    } else {
        for (int i = 0; i < N; i++) {
            answer[(i + cycle) % N] = A[i]; 
        }       
        result.A = answer;
    }
    result.N = N;

    return result;
}
{% endhighlight %}

회전 횟수를 입력받을 `cycle` 변수를 선언하여 회전횟수인 `K`값에 배열 A의 길이인 `N`값을 나눠 주었다. 배열의 길이와 회전 횟수가 같으면 배열 A와 같은 값이 반환하면 되고, 배열의 길이가 5라고 가정할 때, 3, 8, 13번의 회전은 같은 값을 반환해야 하기 때문에 `cycle`변수를 사용하려고 하였다.   

잘못된 부분 : `N = 0`이 되면 `cycle`계산 시 분모가 0이 되어 `RUNTIME ERROR`가 발생하였다.

<br>

## 두번째 - 100점 
{% highlight c linenos %}
struct Results solution(int A[], int N, int K) {
    struct Results result;
    int* answer = (int*)malloc(sizeof(int)*N);    

    if (N == 0){
        result.A = A;
    } else {
        for (int i = 0; i < N; i++) {
            answer[(i + K) % N] = A[i];
        }
        result.A = answer;
    }
    result.N = N;

    return result;
}
{% endhighlight %}

숫자를 회전 시키다 보면 배열의 크기를 넘어가 버리는 상황이 생기게 된다. 배열의 크기를 넘어가게 되면 다시 0번째 자리로 이동을 시켜주어야 하는데 다음의 식을 사용하였다

>(i + K) % N

옮기려는 자리`(i + K)`가 배열의 크기`N`보다 클 경우 `N`으로 나누어 다시 0부터 시작하게 한다.

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}