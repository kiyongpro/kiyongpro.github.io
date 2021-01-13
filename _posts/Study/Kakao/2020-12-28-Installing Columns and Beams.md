---
title:  "[Kakao]2020 KAKAO BLIND RECRUITMENT - 기둥과 보 설치 Java 풀이" 
excerpt: ""

categories:
  - Kakao
tags:
  - [Kakao, Java]
 
toc: false
toc_sticky: false

date: 2020-12-28
last_modified_at:
---
# 문제
---
**기둥과 보 설치 문제 풀기** [바로가기](https://programmers.co.kr/learn/courses/30/lessons/60061 ){:target="_blank"}

<br>

# 풀이 과정
---
- **기둥을 짓는 조건**
    1. y가 0이다.
    2. y가 n보다 작아야한다.
    3. y-1에 기둥이 설치되어있다.
    4. 현재위치 또는 x-1에 보가 설치되어있다.

- **보를 짓는 조건**
    1. y가 0보다 커야한다.
    2. x가 n보다 작아야한다.
    3. y-1 또는 (x+1,y-1)에 기둥이 설치되어있다.
    4. x-1 그리고 x+1에 보가 설치되어있다.

- **기둥 또는 보를 삭제하는 조건**   
    임시로 현재 기둥 또는 보를 삭제한 후, (0, y)부터 (n, n)까지 위 2조건을 성립하는지 확인한다. (하나라도 실패하면 불가능 다시 복원한다.)
<br>

# 결과
---

{% highlight java linenos %}
class Solution {
    public int[][] solution(int n, int[][] build_frame) {        
        Grid grid = new Grid(n+1);  //2차원 격자생성
        int count = 0;  //설치된 구조물의 횟수
        
        for(int i = 0; i < build_frame.length; i++){
            int x = build_frame[i][0];  //x좌표
            int y = build_frame[i][1];  //y좌표
            int kind = build_frame[i][2];   //기둥(0) or 보(1)
            int make = build_frame[i][3];   //제거(0) or 설치(1)
            
            if(make == 0){
                //제거 가능한지 확인
                if(grid.demolish(x, y, kind)){
                    count--;
                }
            }
            else{
                // 설치 가능한지 확인
                if(grid.build(x, y, kind)){
                    count++;
                }
            }           
        }        
        
        //정답을 입력하는 부분
        int[][] answer = new int[count][3];        
        int index = 0;
        loop:for(int x = 0; x <= n; x++){
            for(int y = 0; y <= n; y++){
                if(grid.check(x,y,0))
                    answer[index++] = new int[]{x, y, 0};
                if(grid.check(x,y,1))
                    answer[index++] = new int[]{x, y, 1};
                if(index == count)
                    break loop;
            }
        }        
        
        return answer;
    }
}

class Grid{
    Node[][] nodes;    
    int n;
    Grid(int n){
        this.n = n;
        nodes = new Node[n][n];        
        createNode(n);
    }
    
    void createNode(int n){
        for(int x = 0; x < n; x++){
            for(int y = 0; y < n; y++){
                nodes[x][y] = new Node(x, y);
            }
        }
    }
    
    //설치하는 부분
    public boolean build(int x, int y, int kind){
        Node node = nodes[x][y];
        if(node.pb[kind])
            return false;
        
        node.pb[kind] = true;
        node.pb[kind] = possible(x,y,kind);
        
        return node.pb[kind];        
    }
    
    //제거 하는 부분
    public boolean demolish(int x, int y, int kind){
        Node node = nodes[x][y];
        if(!node.pb[kind])
            return false;        
        
        node.pb[kind] = false;
        loop:for(int xx = 0; xx < n; xx++){
            for(int yy = y; yy < n; yy++){
                if(!possible(xx, yy, 0) || !possible(xx, yy, 1)){
                    node.pb[kind] = true;
                    break loop;
                }                
            }
        }        
        return !node.pb[kind];   
    }

    //설치하기 위한 조건
    public boolean possible(int x, int y, int kind){                
        if(x < 0 || x >= n || y < 0 || y >= n)
            return false;
        
        if(!nodes[x][y].pb[kind])
            return true;
        
        if(kind == 0){
            //기둥을 짓기 위한 조건 
            if(y == 0 || isbuilt(x-1,y,1) || isbuilt(x,y,1) || isbuilt(x,y-1,0))
                return true;
        }
        else{
            //보를 짓기 위한 조건
           if(isbuilt(x,y-1,0) || isbuilt(x+1,y-1,0) || (isbuilt(x-1,y,1) && isbuilt(x+1,y,1)))
               return true;
        }
        return false;
    }
    
    //기둥 또는 보가 설치되어 있는지 확인 하는 부분
    public boolean isbuilt(int x, int y, int kind){        
        if(x < 0 || x >= n || y < 0 || y >= n)
            return false;        
        
        return nodes[x][y].pb[kind];
    }
    
    public boolean check(int x, int y, int kind){        
        return nodes[x][y].pb[kind];
    } 
}

class Node{
    int x;
    int y;
    boolean[] pb = new boolean[2];  //기둥과 보의 설치 유무를 확인
    
    Node(int _x, int _y){
        x = _x;
        y = _y;
        pb[0] = false;
        pb[1] = false;
    }
}
{% endhighlight %}

<br>

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}