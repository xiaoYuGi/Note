字符串哈希

核心思想：将字符串看成一个P进制的数，然后将其转化成十进制的数，并且与一个Q值进行取模运算，这样做的目的是为了可以快速比对字符串是否相同;

一般来说P值取131或13331时，哈希冲突很小。

Q 取  2^64  这是因为hash值在求的过程中会变得非常大，这样的话就会溢出，而64位整数溢出的话就是相当于对2^64取了模，所以用这个值可以不需要再进行取模运算消耗性能。



P数组：为了快速求出整个字符串中任意两点之间的哈希值，需要有一个换算公式；

字符串上任意两点之间的哈希值的求法：

```java
/*
例如字符串  123456中:
h = int[7];
h[1] = hash(1) = 1;
h[2] = hash(12) = 1 * 10 + 2;
h[3] = hash(123) = 1 * 10^2 + 2 * 10 + 3;
h[4] = hash(1234) = 1 * 10^3 + 2 * 10^2 + 3 * 10 + 4;
h[5] = hash(12345) = 1 * 10^4 + 2 * 10^3 + 3 * 10^2 + 4 * 10 + 5;
h[6] = hash(123456) = 1 * 10^5 + 2 * 10^4 + 3 * 10^3 + 4 * 10^2 + 5 * 10 + 6

有了上述数组之后，如果要求字符串 “123456” 中任意长度的子串的hash值应该怎么求？

hash(23) = hash(123) - hash(1) * 10^(2) = h[3] - h[1] ^ (3 - 1);
更一般的:
hash(L~R) = hash(R) - hash(L - 1) * 10^(R - L + 1) 

10^(R - L + 1)  这一段可以用一个数组存下来，其实意义非常简单就是一个进制的的n次方
*/
```

代码模板：
c++
```c++
#include <iostream>
#include <algorithm>

const int N = 100010,base = 131;
typedef unsigned long long ULL;

int n,m;
char s[N];
ULL p[N],h[N];

// 公式
ULL get(int l,int r){
    return h[r] - h[l - 1] * p[r - l + 1];
}

int main(){
    scanf("%d%d%s",&n,&m,s + 1);
    
    p[0] = 1;
    for(int i = 1;i <= n;++i){
        p[i] = p[i - 1] * base;
        h[i] = h[i - 1] * base + s[i];
    }
    
    while(m --){
        int l1,r1,l2,r2;
        scanf("%d%d%d%d",&l1,&r1,&l2,&r2);
        if(get(l1,r1) == get(l2,r2)) puts("Yes");
        else puts("No");
    }
    return 0;
}


```

java
```java
import java.util.*;

public class Main{
    static int N  = 100010, P = 131;
    static long[] h = new long[N];
    static long[] p = new long[N];
    static char[] str;

    static long get(int l, int r){
        return h[r] - h[l - 1] * p[r - l + 1];
    }

    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(), m = sc.nextInt();
        String s = " " + sc.next();
        str = s.toCharArray();
        p[0] = 1;
        for(int i = 1; i <= n; i++){
            p[i] = p[i - 1] * P;
            h[i] = h[i - 1] * P + str[i];
        }
        while(m -- > 0){
            int l1 = sc.nextInt(), r1 = sc.nextInt(), l2 = sc.nextInt(), r2 = sc.nextInt();
            if(get(l1, r1) == get(l2, r2)) System.out.println("Yes");
            else System.out.println("No");
        }
    }
}

```









