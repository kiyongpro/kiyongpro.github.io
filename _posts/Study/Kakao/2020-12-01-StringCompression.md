---
title:  "[Kakao]2020 KAKAO BLIND RECRUITMENT - 문자열 압축 Java 풀이" 
excerpt: ""

categories:
  - Kakao
tags:
  - [Kakao, Java]
 
toc: false
toc_sticky: false

date: 2020-11-10
last_modified_at:
---

**2020 Kakao BLIND RECRUITMENT** [바로가기](https://tech.kakao.com/2019/10/02/kakao-blind-recruitment-2020-round1/) 
{: .notice--warning}

---
# 문제 해석
---
> abcabcabcabcdededededede (24)

- 1개 단위 => abcabcabcabcdededededede (24)
- 2개 단위 => ab/ca/bc/ab/ca/bc/6de (15)
- 3개 단위 => 4abc/ded/ede/ded/ede (16)
- 4개 단위 => abca/bcab/cabc/3dede (17)
- 5개 단위 => abcab/cabca/bcded/edede/dede (24)
- 6개 단위 => 2abcabc/2dedede (14)

> xababcdcdababcdcd (17)

- x/ababcdcd/ababcdcd (1/8/8 불가능) => xababcdc/dababcdc/d (8/8/1 가능)
- k개로 나누어줄 때, 맨마지막 단위가 k보다 작다면 옆에 붙여준다.

<br>

# 풀이 과정
---
1. 1 ~ N/2 까지의 단위로 쪼개어 압축을 해준다.(N = 24, 1 ~ 12 까지 계산)
2. k와 k+1 문자열을 비교하여 같은 값이 나오면 count를 하나 더해준다. count가 2이상이면 count + k번째 문자열을 더해준다.
    - abcabcabcabcdededededede (24)
    - 1개 단위 0 : 'a', 1 : 'b', 2: 'c' ... 23 : 'e'
    - 3개 단위 0 : 'abc', 2 : 'abc', 3 : 'abc' ... 7 : 'ede' 

<br>

# 결과
---

{% highlight java linenos %}
class Solution {
    public int solution(String s) {        
        int len = s.length() / 2;        
        int answer = s.length();
        
        // 1부터 N/2 까지의 단위 반복
        for(int range = 1; range<=len; range++){
            String resultString = ""; //압축된 문자열           
            int start = 0;            //문자열 시작지점

            // 문자열 전체를 검색
            while(start < s.length()){
                String sCompare = slice(s,start,range); // k번째 문자열
                int iCompare = 0;       // 중복 횟수
                                       
                do{
                    iCompare++;
                    start += range;

                    //시작지점이 문자열의 길이보다 넘어가면 반복 중지
                    if(start >= s.length())
                        break;
                }while(sCompare.equals(slice(s,start,range)));

                //중복 문자열이 1이면 count 생략
                if(iCompare != 1)
                    resultString += iCompare;                    
                resultString += sCompare;

                //현재 가장작은 길이로 압축된 문자열과 진행중인 문자열의 길이를 비교              
                if(resultString.length() > answer){
                    break;
                }
            }
            if(resultString.length() < answer){
                answer = resultString.length();
            }
        }        
        return answer;
    }

    //문자열 나누는 함수
    public String slice(String s, int a, int b){
        String temp = "";
        if(a+b < s.length())
            temp = s.substring(a, a+b);
        else
            temp = s.substring(a);
        
        return temp;
    }
}
{% endhighlight %}

<br>

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}