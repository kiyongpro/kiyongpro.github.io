---
title:  "[Kakao]2020 KAKAO BLIND RECRUITMENT - 가사 검색 Java 풀이" 
excerpt: ""

categories:
  - Kakao
tags:
  - [Kakao, Java]
 
toc: false
toc_sticky: false

date: 2020-12-21
last_modified_at:
---
# 문제
---
**가사 검색 문제 풀기** [바로가기](https://programmers.co.kr/learn/courses/30/lessons/60060 ){:target="_blank"}

<br>

# 문제 해석
---
Trie 알고리즘을 활용하는 문제이다.   
**참고** [바로가기](https://ko.wikipedia.org/wiki/%ED%8A%B8%EB%9D%BC%EC%9D%B4_(%EC%BB%B4%ED%93%A8%ED%8C%85)){:target="_blank"}

<br>

# 풀이 과정
---
1. **단어의 길이별 각각의 노드를 생성합니다.**   
![trie01](https://user-images.githubusercontent.com/33146320/104425676-4c7acf80-55c4-11eb-994a-60cd5a8c9f70.png){: width="200" height="100"}
2. **words의 단어들을 입력한다.**   
["frodo", "front", "frost", "frozen", "frame", "kakao"]   
![trie02](https://user-images.githubusercontent.com/33146320/104430626-45ef5680-55ca-11eb-8161-ec95b4d3cf04.png){: width="400" height="100"}
3. **'fro??'는 5글자이므로 5의 'f-r-o'값인 3이 정답이된다.** 

<br>

# 결과
---

{% highlight java linenos %}
import java.util.*;

class Solution {
    public int[] solution(String[] words, String[] queries) {
        Trie[] tries = new Trie[100001];
        
        int[] answer = new int[queries.length];
        
        //Trie 자료구조 생성
        for(String s : words){
            int len = s.length();
            if(tries[len] == null) 
                tries[len] = new Trie();
            tries[len].insert(s);
        }
        
        //Trie 불러오기
        for(int i = 0; i < queries.length; i++){
            int len = queries[i].length();
            if(tries[len] == null)
                answer[i] = 0;            
            else
                answer[i] = tries[len].getCount(queries[i]);            
        }
        
        return answer;
    }
}

class Trie{
    TrieNode pre_Node;  //앞자리부터의 배열
    TrieNode suf_Node;  //뒷자리부터의 배열
    
    Trie(){
        pre_Node = new TrieNode();
        suf_Node = new TrieNode();
    }
    
    public void insert(String word){
        TrieNode pre_Node = this.pre_Node;
        TrieNode suf_Node = this.suf_Node;
        
        for(int i = 0; i< word.length(); i++){
            pre_Node.count++;
            //HashMap의 computeIfAbsent를 사용하여 word(charAt(i))를 주소로 가지고있는 TrieNode를 가지고 온다.
            //만약 null값이 나오면 새로 생성하여 가지고 온다. [c->new TrieNode()]부분
            pre_Node = pre_Node.children.computeIfAbsent(word.charAt(i), c ->new TrieNode());
        }        
        for(int i = word.length()-1; i >= 0; i--){
            suf_Node.count++;
            suf_Node = suf_Node.children.computeIfAbsent(word.charAt(i), c ->new TrieNode());            
        }
    }
    
    public int getCount(String word){
        //맨 앞자리가 '?'면 역방향 배열 아니면 정방향 배열
        if (word.charAt(0) == '?')
            return getCountBack(word);        
        else
            return getCountFront(word);        
    }
    
    //정방향 배열
    public int getCountFront(String word){        
        TrieNode pre_Node = this.pre_Node;
        for(int i = 0; i< word.length(); i++){
            if(word.charAt(i) == '?') break;
            if(!pre_Node.children.containsKey(word.charAt(i))) return 0;
            pre_Node = pre_Node.children.get(word.charAt(i));                
        }
        
        return pre_Node.count;
    }

    //역방향 배열
    public int getCountBack(String word){        
        TrieNode suf_Node = this.suf_Node;
        for(int i = word.length()-1; i >= 0; i--){
            if(word.charAt(i) == '?') break;
            if(!suf_Node.children.containsKey(word.charAt(i))) return 0;
            suf_Node = suf_Node.children.get(word.charAt(i));
        }
        
        return suf_Node.count;
    }
}

class TrieNode{ 
    Map<Character, TrieNode> children; 
    int count; 
    
    TrieNode(){ 
        this.children = new HashMap<>(); 
        this.count = 0; 
    } 
}
{% endhighlight %}

<br>

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}