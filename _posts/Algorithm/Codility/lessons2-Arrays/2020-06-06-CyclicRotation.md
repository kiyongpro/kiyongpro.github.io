---
title:  "[Codility] Lesson2. Arrays-CyclicRotation C언어 풀이" 
excerpt: "Codility c언어 문제 풀이 2-1"

categories:
  - Algorithm
tags:
  - [Algorithm, Codility, C, malloc]

toc: false
toc_sticky: false

date: 2020-06-06
last_modified_at:
---
Codility 두 번째 Lesson의 이름은 Arrays(배열)입니다. 배열은 많은 항목을 한 곳에 저장하는 데 사용할 수 있는 데이터 구조입니다. 대형마트에서 쇼핑을 한다고 할 때, 하나의 장바구니에 하나의 제품만을 보관하지 않는 것과 같습니다. 그렇지 않다면 10개의 제품을 구매하였을 때, 우리는 10개의 장바구니를 들고 다녀야 하는 상황이 발생하게 됩니다.

---
# 1. 문제

정수 N으로 구성된 배열 A를 K값 만큼 회전 시켜주면 되는 문제이다.   
예를 들어, A = [3,8,9,7,6], K = 3 일 때, [9,7,6,3,8] 값을 리턴해주면 된다.

<br>

# 2. 풀이

1. K = 3일 때, 한 번에 한 칸씩 3번을 이동하기보다, K값만큼 한 번에 이동한다.

<br>

# 3. 정답
## 첫번째 - 87점
{% highlight c linenos %}
struct Results solution(int A[], int N, int K) {
    struct Results result;
    int cycle = K % N;
    int* answer = (int*)malloc(sizeof(int) * N);

    result.N = N;

    if (cycle == 0)
        result.A = A;
    else {
        for (int i = 0; i < N; i++) 
            answer[(i + cycle) % N] = A[i];        
        result.A = answer;
    }
    return result;
}
{% endhighlight %}

- **3Line** - 이동 칸수를 결정하는 변수이다.
- **4Line** - 정답을 입력할 배열을 `malloc`함수를 통하여 생성하였다. 이 함수의 인자는 데이터의 크기를 의미한다. `int`의 크기를 N만큼 할당해 주었다.
- **8Line** - `cycle = 0`이면 이동이 없다는 뜻이다. A를 그대로 반환해주었다.
- **12Line** - `cycle`값만큼의 이동을 해주는 코드이다. A의 배열 크기보다 커지면 0 값으로 이동한다.

잘못된 부분 : 배열에 빈값이 들어왔을 때 `RUNTIME ERROR`가 발생하였다.

<br>

## 두번째 - 100점 
{% highlight c linenos %}
struct Results solution(int A[], int N, int K) {
    struct Results result;
    int* temp = (int*)malloc(sizeof(int)*N);

    result.N = N;

    if (N == 0){
        result.A = A;
    }
    else {
        for (int i = 0; i < N; i++) {
            temp[(i + K) % N] = A[i];
        }
        result.A = temp;
    }
    return result;
}
{% endhighlight %}

N이 0일 때, 나머지를 구하게 되면 오류가 생겨서 `cycle`부분을 없애고, 7번 부분을 고쳐 주었다. 


[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}