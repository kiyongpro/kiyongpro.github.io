---
title:  "[Codility] Lesson6. Sorting-MaxProductOfThree C언어 풀이" 

categories:
  - Codility
tags:
  - [Codility, C]
 
toc: false
toc_sticky: false

date: 2020-08-20
last_modified_at:
---
# 1. 문제
---
길이가 N인 배열 A가 주어졌을 때, **3개의 원소를 곱해서 가장 큰 수를 반환하는 문제**

>예제   
A[0] = -3   
A[1] = 1   
A[2] = 2   
A[3] = -2   
A[4] = 5   
A[5] = 6   

- (0, 1, 2) : -3 * 1 * 2 = -6
- (1, 2, 4) : 1 * 2 * 5 = 10
- (2, 4, 5) : 2 * 5 * 6 = 60

3개의 곱 중 가장 큰 `60`을 반환해 준다.

<br>

# 2. 정답
## 첫번째 - 100점
>O(N * log(N))

{% highlight c linenos %}
void swap(int* data, int index1, int index2)
{
    int temp = data[index1];
    data[index1] = data[index2];
    data[index2] = temp;
}

void quickSort(int* data, int left, int right) 
{
    int pivotValue = data[(left + right) / 2];
    int i = left;
    int j = right;

    while (i <= j)
    {
        while (data[i] < pivotValue) i++;
        while (data[j] > pivotValue) j--;
        if (i <= j)
        {
            swap(data, i, j);
            i++;
            j--;
        }
    }
    if (left < j)
        quickSort(data, left, j);    
    if (right > i)
        quickSort(data, i, right);    
}
int solution(int A[], int N) {
    
    quickSort(A, 0, N-1);
    
    int frontMul = A[0] * A[1] * A[N-1];
    int rearMul = A[N-1] * A[N-2] * A[N-3];
    
    return frontMul > rearMul ? frontMul : rearMul;
}
{% endhighlight %}

오름차순 정렬이 되어 있다고 가정할 시, 가장 큰 수가 나오는 방법은 2가지가 있다.

1. 가장 큰 3개의 수의 곱
2. 가장 작은 2개의 수와 가장 큰 1개의 수의 곱

원소에 음수가 포함되어있지 않다면 1번이 확실하지만, 음수가 포함되어 있음므로 2번의 과정도 확인하여야 한다.

퀵 정렬(Quick Sort)을 사용해서 A를 정렬한 뒤, 1번과 2번의 수를 비교하여 가장 큰 수를 반환해 준다.

<br>

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}