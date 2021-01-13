---
title:  "[Kakao]2020 KAKAO BLIND RECRUITMENT - 자물쇠와 열쇠 Java 풀이" 
excerpt: ""

categories:
  - Kakao
tags:
  - [Kakao, Java]
 
toc: false
toc_sticky: false

date: 2020-12-14
last_modified_at: 2020-12-21
---

# 문제 해석
---
격자의 크기가 **1x1** 으로 이루어진 **NxN** 크기의 자물쇠와 **MxM** 크기의 열쇠가 있다.   
자물쇠의 홈이 파여있는데 열쇠를 사용하여 모든 홈을 없애면 열리게 되어있다. (열쇠는 회전과 이동이 가능)

![그림1](https://grepp-programmers.s3.amazonaws.com/files/production/469703690b/79f2f473-5d13-47b9-96e0-a10e17b7d49a.jpg)

<br>

# 풀이 과정
---
1. 자물쇠를 열 수 있는 모든 경우의 수는 4 * (N + M - 1)^2 가 된다.
2. N+M-1은 열쇠가 한쪽 방향으로만 움직일 때의 경우의 수이다. 두쪽 방향을 이동하기 위해서 ^2을 준다. (반복문 2개사용)
3. 4는 열쇠의 회전방향 할 수있는 수이다.(0, 90, 180, 270) 회전하는 메소드를 만들어 회전 시켜준다.(반복문 1개사용)

<br>

# 결과
---

{% highlight java linenos %}
class Solution {
    public boolean solution(int[][] key, int[][] lock) {
        int N = lock.length;
        int M = key.length;
        
        int concave = 0;
        
        //총 홈의 갯수를 파악한다.
        for(int[] a : lock)
            for(int b : a)
                if(b == 0)
                    concave++;  //자물쇠 홈의 갯수

        //열쇠에 관한 부분
        //4방향 계산
        for(int R = 0; R < 4; R++){
            //세로 방향 이동
            for(int V = -M+1; V < N; V++){
                //가로 방향 이동
                skip:for(int H = -M+1; H < N; H++){ 
                    int convex = 0; //열쇠가 홈을 채우는 개수
                    for(int i = V > 0 ? V : 0; i < ((M+V < N) ? M+V : N); i++){   
                        for(int j = H > 0 ? H : 0; j < ((M+H < N) ? M+H : N); j++){
                            //열쇠가 자물쇠의 홈을 채우면 참
                            if(lock[i][j]== 0 && key[-V+i][-H+j]==1){
                                convex++;
                            } 
                            //자물쇠의 홈을 채우지 못하였거나, 홈이 아닌 곳에 열쇠가 존재하면 스킵
                            else if(lock[i][j] == key[-V+i][-H+j]){
                                continue skip;
                            }
                        }
                    }
                    //자물쇠의 홈을 모두 채웠으면 성공
                    if(convex == concave)
                        return true;                    
                }            
            }
            //열쇠를 회전시킨다.
            key = rotate(key);
        }
        
        return false;
    }

    //열쇠를 회전 하는 부분
    public int[][] rotate(int[][] data) {
        int n = data.length;
        int[][] rotate = new int[n][n];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                rotate[i][j] = data[n-1-j][i];
            }
        }
        return rotate;
    }
}
{% endhighlight %}

<br>

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}