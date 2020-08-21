---
title:  "[Codility] Lesson6. Sorting-NumberOfDiscIntersections C언어 풀이" 

categories:
  - Codility
tags:
  - [Codility, C]
 
toc: false
toc_sticky: false

date: 2020-08-21
last_modified_at:
---
# 1. 문제
---
원의 중심이 (K, 0) 이고, 반지름이 A[k]인 원 N개가 주어 졌을 때, **겹치는 원의 개수를 반환하는 문제이다.**

>예제   
A[0] = 1   
A[1] = 5   
A[2] = 2   
A[3] = 1   
A[4] = 4   
A[5] = 0   

이런 모양의 그림이 나오게 된다.   
![1](https://user-images.githubusercontent.com/33146320/90871467-17cc6880-e3d6-11ea-939f-a6c83d20b2c8.png){: width="300" height="150"}  

<details>
<summary>이미지 해설 접기/펼치기</summary>
<div markdown="1">

## K = 0 일 때 (기준 빨간색, 겹치는 원 파란색)   
![2](https://user-images.githubusercontent.com/33146320/90871470-1a2ec280-e3d6-11ea-8599-dafd8fb567c0.png){: width="300" height="150"}   
겹치는 원의 숫자가 3개이다. k = 0은 제외 시킨다.

## k = 1 일 때   
![3](https://user-images.githubusercontent.com/33146320/90871474-1ac75900-e3d6-11ea-9b8f-153f7990f08a.png){: width="300" height="150"}   
겹치는 원의 숫자가 4개이다. 3 + 4 = 7

## k = 2 일 때   
![4](https://user-images.githubusercontent.com/33146320/90871476-1b5fef80-e3d6-11ea-9c79-4f7b38083560.png){: width="300" height="150"}   
겹치는 원의 숫자가 2개이다. 7 + 2 = 9

## k = 3 일 때   
![5](https://user-images.githubusercontent.com/33146320/90871483-1d29b300-e3d6-11ea-97e4-b4d61d7faf99.png){: width="300" height="150"}   
겹치는 원의 숫자가 1개이다. 9 + 1 = 10

## k = 4 일 때   
![6](https://user-images.githubusercontent.com/33146320/90871495-21ee6700-e3d6-11ea-823a-b309c73addf4.png){: width="300" height="150"}   
겹치는 원의 숫자가 1개이다. 10 + 1 = 11

## k = 5 일 때   
![7](https://user-images.githubusercontent.com/33146320/90871513-287cde80-e3d6-11ea-9e38-0076989a94dc.png){: width="300" height="150"}   
겹치는 원의 숫자가 0개이다. 답은 `11`이 된다.

</div>
</details>
<br>

# 2. 정답
## 첫번째 - 100점
>O(N*log(N)) or O(N)

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
    int* discS = (int*)malloc(sizeof(int) * N);
    int* discE = (int*)malloc(sizeof(int) * N);
    
    for(int i = 0; i < N; i++){
        discS[i] = i > A[i] ? i-A[i] : 0;
        discE[i] = N-i-1 > A[i] ? i+A[i] : N-1;
    }
    quickSort(discS , 0, N-1);
    quickSort(discE , 0, N-1);
    
    int s = 0, e = 0, c = 0, result = 0;
    while(e < N){
        if(s < N && discS[s] <= discE[e]){
            c++;
            s++;
        }else{
            result += --c;
            e++;
        }
    }    
    return result < 10000001 ? result : -1;
}
{% endhighlight %}

### 36 ~ 37Line
원의 크기가 0 ~ N-1 범위를 벗어 나는걸 방지하기 위한 부분   
원소의 숫자가 int의 범위를 벗어나는 걸 방지하기 위해서 사용했다.

### 43Line
1. s[0] <= e[0]  c = 1   
![1](https://user-images.githubusercontent.com/33146320/90874198-595f1280-e3da-11ea-8507-9ff7c48c4a44.png){: width="300" height="150"}

<br>

- s[1] <= e[0]  c = 2   
![2](https://user-images.githubusercontent.com/33146320/90874199-59f7a900-e3da-11ea-981f-e587920ffdab.png){: width="300" height="150"}

<br>

- s[2,3] <= e[0]>  c = 4   
![3](https://user-images.githubusercontent.com/33146320/90874200-5a903f80-e3da-11ea-8146-575445796880.png){: width="300" height="150"}

<br>

- s[4] > e[0] (c = 3, reslut += c = 3)   
s[4] <= e[1] c = 4   
![4](https://user-images.githubusercontent.com/33146320/90874204-5b28d600-e3da-11ea-8f46-990eff8b0593.png){: width="300" height="150"}

<br>

- s[5] > e[1] (c = 3, reslut += c = 6)   
s[5] > e[2] (c = 2, reslut += c = 8)   
s[5] <= e[3] c = 3   
![5](https://user-images.githubusercontent.com/33146320/90874206-5b28d600-e3da-11ea-83b0-9bf1d6fb74f5.png){: width="300" height="150"}

<br>

- e[4] (c = 2, reslut += c = 10) (s[6]은 없으므로 비교X)   
![6](https://user-images.githubusercontent.com/33146320/90874207-5bc16c80-e3da-11ea-928d-699d90abba7d.png){: width="300" height="150"}

<br>

- e[5] (c = 1, reslut += c = 11)   
![7](https://user-images.githubusercontent.com/33146320/90874208-5bc16c80-e3da-11ea-9b9f-9e4245c5e99c.png){: width="300" height="150"}

<br>

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}