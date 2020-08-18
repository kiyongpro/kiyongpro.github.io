---
title:  "[코딩도장] Spiral Array C#문제풀이" 

categories:
  - 코딩도장
tags:
  - [코딩도장, C#]
 
toc: false
toc_sticky: false

date: 2020-07-28
last_modified_at:
---


# 1. 문제
> LV.3

>6 6   
  0   1   2   3   4   5   
 19  20  21  22  23   6   
 18  31  32  33  24   7   
 17  30  35  34  25   8   
 16  29  28  27  26   9   
 15  14  13  12  11  10    

위 처럼 6 6이라는 입력을 주면 6x6 매트릭스에 나선형 회전을 한 값을 출력

# 2. 풀이

## 첫번째
{% highlight cs linenos %}
static void Main(string[] args)
{
    string[] input = Console.ReadLine().Split(' ');
    int x = int.Parse(input[1]), y = int.Parse(input[0]);
    int[,] n = new int[x,y];
    int maxX = x - 1, maxY = y - 1;
    int max, count = 0, cycle = 0;

    int xx = 0, yy = 0;
    bool forward = true;
    while (true)
    {
        max = maxY > 1 ? maxY : 1;
        for (int i = 0; i < max; i++)
        {
            n[xx + cycle, yy + cycle] = count++;
            if (forward) yy++;
            else yy--;
        }
        if (count >= x * y) break;

        max = maxX > 1 ? maxX : 1;
        for (int i = 0; i < max; i++)
        {
            n[xx + cycle, yy + cycle] = count++;
            if (forward) xx++;
            else xx--;
        }
        if (count >= x * y) break;                

        forward = !forward;
        if (forward)
        {
            cycle++;
            maxX -= 2;
            maxY -= 2;
        }
        
    }
    count = 0;
    foreach(int num in n)
    {
        Console.Write(num + "\t");
        count++;
        if(count == y)
        {
            Console.WriteLine();
            count = 0;
        }
    }            
}
{% endhighlight %}
 
가로와 세로의 길이가 **6 x 6**이라고 가정 할 때,

>첫번째 회전   
![그림1](https://user-images.githubusercontent.com/33146320/88659500-1f1e9000-d110-11ea-82da-639c1c38ad5f.png) 

>두번째 회전   
![그림2](https://user-images.githubusercontent.com/33146320/88659752-863c4480-d110-11ea-9688-dd2076313fcd.png)

위 그림과 같은 규칙으로 숫자가 생성된다.

첫번째 숫자가 가로(y)를 두번째 숫자가 세로(x)일 때, 이차원 배열 n[x, y]형식의 변수가 생성된다.

- 첫번째 회전   
1. y축 크기를 1씩 y-1번 증가시킨다(y++)   
=> [0,0], [0,1], [0,2], [0,3], [0,4], y를 1번 증가시킨다(입력 X) => [0,5]
1. x축 크기를 1씩 x-1번 증가시킨다(x++)  
=> [0,5], [1,5], [2,5], [3,5], [4,5], x를 1번 증가시킨다(입력 X) => [5,5]
1. y축 크기를 1씩 y-1번 감소시킨다(y--)   
=> [5,5], [5,4], [5,3], [5,2], [5,1], x를 1번 증가시킨다(입력 X) => [5,0]
1. x축 크기를 1씩 x-1번 감소시킨다(x--).
=> [5,0], [4,0], [3,0], [2,0], [1,0], x를 1번 증가시킨다(입력 X) => [0,0]
1. cycle 변수를 생성하여 회전 횟수를 더해준다. => cycle = 1

- 두번째 회전   
두번째 회전부터는 반복횟수를 2씩 감소시켜야 한다. 
x, y에 cycle크기 만큼 더해준다.  
1. y축 크기를 1씩 y-3번 증가시킨다(y++)   
=> [1,1], [1,2], [1,3], y를 1번 증가시킨다(입력 X) => [1,4]
1. x축 크기를 1씩 x-3번 증가시킨다(x++)  
=> [1,4], [2,4], [3,4], y를 1번 증가시킨다(입력 X) => [4,4]
1. y축 크기를 1씩 y-3번 감소시킨다(y--)   
=> [4,4], [4,3], [4,2], y를 1번 증가시킨다(입력 X) => [4,1]
1. x축 크기를 1씩 x-3번 감소시킨다(x--).
=> [4,1], [3,1], [2,1], y를 1번 증가시킨다(입력 X) => [1,1]
1. cycle = 2


위 과정을 반복하면서 각각 배열에 0부터 (x*y-1)크기 까지의 숫자를 입력한다.


처음 문제를 보았을 때는 lv3에 비해서 쉬워 보였는데 생각처럼 깔끔하게 코딩이 안되었다. 

## 두번째(다른사람 풀이)

{% highlight cs linenos %}
static void Main(string[] args)
{
    var input = Console.ReadLine().Split(' ');
    int W = int.Parse(input[1]), H = int.Parse(input[0]);

    int[] arr = new int[W * H], dist = new[] { 1, W, -1, -W };
    int i = -1, j = 0, k = -1, cnt = 0, w = W;

    while (cnt-- > 1 || (cnt = ++k % 2 == 0 ? W-- : --H) > 0)
        arr[i += dist[k % 4]] = j++;

    for (i = 0; i < arr.Length; i++)
        Console.Write("{0,3}" + ((i + 1) % w == 0 ? "\n" : " "), arr[i]);
}
{% endhighlight %}

제일 인상적이었던 풀이방법이다. while 반복문으로 이렇게 할 수 있다는게 세삼 놀라웠다.

```cs
//     1             2
while (cnt-- > 1 || (cnt = ++k % 2 == 0 ? W-- : --H) > 0)
 //    3    
    arr[i += dist[k % 4]] = j++;
```
1번이 false가 나오면 2번의 조건을 확인한 뒤 3번을 하거나 빠져나간다.   
1번의 값이 true 가 나오면 바로 3번으로 이동한다.


[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}