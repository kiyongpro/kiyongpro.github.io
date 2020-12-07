---
title:  "[Kakao]2020 KAKAO BLIND RECRUITMENT - 괄호 변환 Java 풀이" 
excerpt: ""

categories:
  - Kakao
tags:
  - [Kakao, Java]
 
toc: false
toc_sticky: false

date: 2020-12-07
last_modified_at:
---

# 문제 해석
---
'(' 와 ')' 로 이루어진 문자열이 주어진다. '(' 의 개수와 ')' 의 개수가 같다면 이를 **균형잡힌 괄호 문자열**이라고 부릅니다.   
'('와 ')'의 괄호의 짝도 모두 맞을 경우에는 이를 **올바른 괄호 문자열**이라고 부릅니다.   
>"(()))(" -> 균형잡힌 괄호 문자열 O, 올바른 괄호 문자열 X   
"(())()" -> 균형잡힌 괄호 문자열 O, 올바른 괄호 문자열 O 

'(' 와 ')' 로만 이루어진 문자열 w가 균형잡힌 괄호 문자열 이라면 다음과 같은 과정을 통해 **올바른 괄호 문자열로 변환하여 반환하는 문제**

### 변환과정
1. 입력이 빈 문자열인 경우, 빈 문자열을 반환합니다. 
2. 문자열 w를 두 "균형잡힌 괄호 문자열" u, v로 분리합니다. 단, u는 "균형잡힌 괄호 문자열"로 더 이상 분리할 수 없어야 하며, v는 빈 문자열이 될 수 있습니다. 
3. 문자열 u가 "올바른 괄호 문자열" 이라면 문자열 v에 대해 1단계부터 다시 수행합니다. 
  3-1. 수행한 결과 문자열을 u에 이어 붙인 후 반환합니다. 
4. 문자열 u가 "올바른 괄호 문자열"이 아니라면 아래 과정을 수행합니다.   
  4-1. 빈 문자열에 첫 번째 문자로 '('를 붙입니다.   
  4-2. 문자열 v에 대해 1단계부터 재귀적으로 수행한 결과 문자열을 이어 붙입니다.   
  4-3. ')'를 다시 붙입니다.   
  4-4. u의 첫 번째와 마지막 문자를 제거하고, 나머지 문자열의 괄호 방향을 뒤집어서 뒤에 붙입니다.   
  4-5. 생성된 문자열을 반환합니다.

<br>

# 풀이 과정
---
1. 맨처음 문자를 기준으로 한쌍의 괄호를 스택을 사용하여 나누어 줍니다.   
"(()))(" => u = (()) v = )(
"))((()" => u = ))(( v = ()
2. v를 1번과정을 v가 나오지 않을 때까지 재귀합니다.   
"(()))(" => u = (()) v = )(   
")("     => u2 = )( v2 = null
3. u가 올바른 형식이라면 `3번`을 아니면 `4번` 과정을 해줍니다.

<br>

# 결과
---

{% highlight java linenos %}
class Solution {
    public String solution(String p) {
        String answer = "";
        answer = calc(p);
        
        return answer;
    }    
    public String calc(String p){
        //비교할 첫번째 문자
        char compare = p.charAt(0);
        int top = 0;
        int index = 1;
        
        //스택형식을 사용 가져올 데이터가 없거나 문자열 w의 길이보다 크면 빠져나온다.
        while(top != -1 && index < p.length()){
            if(compare == p.charAt(index++))            
                top++;            
            else 
                top--;
        }
        String u = p.substring(0, index);
        //v가 비어있지 않으면 재귀
        String v = index < p.length() ? calc(p.substring(index, p.length())) : "";    

        //u가 올바르지 않을 때
        if(compare == ')'){
            String temp = '(' + v + ')';
            //u의 앞뒤 문자열을 제외한 문자를 뒤집어 준다.
            for(int i = 1; i < index-1; i++){
                char c = u.charAt(i);
                if(c == '(')
                    temp +=')';
                else
                    temp +='(';                            
            }  
            u = temp;
        }
        //u가 올바를 때
        else
            u += v;             
        
        return u;
    }
}
{% endhighlight %}

<br>

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}