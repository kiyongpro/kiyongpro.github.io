---
title:  "[Codility] Lesson5. PrefixSums-MinAvgTwoSlice C언어 풀이" 
excerpt: "Codility c언어 문제 풀이 5-3"

categories:
  - Study
tags:
  - [Codility, C]
 
toc: false
toc_sticky: false

date: 2020-06-16
last_modified_at:
---
# 1. 문제
---
Slice(P,Q)의 평균이 가장 작을 때, P를 반환하는 문제이다.
> 예시    
A[0] = 4   
A[1] = 2   
A[2] = 2   
A[3] = 5   
A[4] = 1   
A[5] = 5   
A[6] = 8   

- slice(1, 2), (2 + 2) / 2 = 2;
- slice(3, 4), (5 + 1) / 2 = 3;
- slice(1, 4), (2 + 2 + 5 + 1) / 4 = 2.5.

평균이 가장 작은 slice(1,2)의 1을 반환해야 한다.

<br>

# 2. 정답
## 첫번째 - 60점
>시간 복잡도 : O(N**2)

{% highlight c linenos %}
int solution(int A[], int N) {    
    int sum = 0;
    int minNum = N;
    double minAvg = 10000;
    
    for(int i = 0; i < N-1; i++){
        sum = A[i];
        for(int j = i+1; j < N; j++){
            sum += A[j];
            if((double)sum/(double)(j-i+1) < minAvg){
                minAvg = (double)sum/(double)(j-i+1);
                minNum = i;
            }
        }
    }
    return minNum;
}
{% endhighlight %}

일단 생각나는대로 코딩을 해보았다. (0,1), (0,2), (0,3) ... (1,2), (1,3) ... (N-2, N-1)까지 평균 다 구하고 제일 적은 값을 내는 방식이다. 역시나 `TIMEOUT ERROR`를 발생하였다.

## 두번째 - 100점(다른사람 풀이)
>시간 복잡도 : O(N)

{% highlight c linenos %}
int solution(int A[], int N) {
    if (N == 2) return 0;

    int minSliceTwo = A[0] + A[1];
    int minTwoIndex = 0;

    int minSliceThree = 10000;
    int minThreeIndex = 0;

    for (int i = 2; i < N; i++) {
        int sliceTwo = A[i - 1] + A[i];
        if (sliceTwo < minSliceTwo) {
            minSliceTwo = sliceTwo;
            minTwoIndex = i - 1;
        }

        int sliceThree = sliceTwo + A[i - 2];
        if (sliceThree < minSliceThree) {
            minSliceThree = sliceThree;
            minThreeIndex = i - 2;
        }
    }
    int averageMinTwo = minSliceTwo*3;
    int averageMinThree = minSliceThree*2;

    if (averageMinTwo == averageMinThree) 
        return minTwoIndex < minThreeIndex ? minTwoIndex : minThreeIndex;
    else 
        return averageMinTwo < averageMinThree ? minTwoIndex : minThreeIndex;
{% endhighlight %}

검색을 통해 찾아본 결과 문제가 수학적인 이해가 필요한 문제였다. 결론은 가장 작은 평균은 2개의 숫자 또는 3개의 숫자로 이루어져 있다는 것이다.

- (a,b,c,d) 라는 4개의 숫자가 있을 때, (a,b,c,d)의 평균은 (ab, cd)의 평균과 같다. 
- ab < cd 라고 하면 ab < abcd < cd 가 되어 ab가 가장 작은 평균을 가지고 있다는 이야기가 된다.
- 예외적으로 3개의 인자만을 가지고 있다면 위의 방법이 틀릴 수도 있어 3개의 값도 따로 계산하여야 한다.


[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}