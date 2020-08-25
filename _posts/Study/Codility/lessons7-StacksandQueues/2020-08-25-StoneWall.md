---
title:  "[Codility] Lesson7. Stacks and Queues-StoneWall C언어 풀이" 

categories:
  - Codility
tags:
  - [Codility, C]
 
toc: false
toc_sticky: false

date: 2020-08-25
last_modified_at:
---
# 1. 문제
--- 
k번째 돌벽의 높이를 가지고 있는 H[k]배열이 주어 질 때, **가장 최소한의 돌로 성벽을 쌓는 문제**

>예제   
H[0] = 8    H[1] = 8    H[2] = 5   
H[3] = 7    H[4] = 9    H[5] = 8   
H[6] = 7    H[7] = 4    H[8] = 8    

![](https://codility-frontend-prod.s3.amazonaws.com/media/task_static/stone_wall/static/images/auto/4f1cef49cc46d451e88109d449ab7975.png)

총 `7`개의 돌로 성벽을 쌓았다.

<br>

# 2. 정답
## 첫번째 - 100점
>O(N)

{% highlight c linenos %}
int solution(int H[], int N) {
    int *stack = (int*)malloc(sizeof(int)*N);
    int top = 0, count = 1;
    
    stack[0] = H[0];
    
    for(int i = 1; i < N; i++){
        for(;stack[top] > H[i]; top--){
            if(top == 0){
                stack[top] = H[i];
                count++;
                break;
            }
        }
        if(stack[top] < H[i]){
            count++;
            stack[++top] = H[i];
        }
    }
    return count;
}
{% endhighlight %}
- Lien8   
H[k] < stack[top]이면 `top--` 한다 이 과정을 반복한다.   
 `top==0`이 되면, stack[top] = H[k]가 된다. 이때 돌의 개수가 하나 **증가**한다.   
- Line15   
H[k] > stack[top]이면 stack[top+1] =  H[k]가 된다. 이때 돌의 개수가 하나 **증가**한다.  
- Skip   
H[k] == stack[top]이면 넘어간다.

<br>

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}