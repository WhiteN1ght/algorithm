## 12. Integer to Roman

### 1.  题目信息：

题目地址：https://leetcode.com/problems/integer-to-roman/

**题目描述：**

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

For example, two is written as `II` in Roman numeral, just two one's added together. Twelve is written as, `XII`, which is simply `X` + `II`. The number twenty seven is written as `XXVII`, which is `XX` + `V` + `II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:

- `I` can be placed before `V` (5) and `X` (10) to make 4 and 9. 
- `X` can be placed before `L` (50) and `C` (100) to make 40 and 90. 
- `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.

Given an integer, convert it to a roman numeral. Input is guaranteed to be within the range from 1 to 3999.

大意为将给出的1–3999范围内的整数，转换为罗马数字型

### 2.  解题代码：

自己写的c代码，这道题开始想用非枚举的方式来做，然而看来枚举方式更简单一些。

```c
#define ROMAN_SUM_TYPE_COUNT 13

struct RomanItem
{
    int interSum;
    char *romanStr;
};

char* intToRoman(int num) {
    char *answer = (char *)malloc(sizeof(char) * 50);
    answer[0] = '\0';
    int quotient = 0;
    struct RomanItem romanArray[ROMAN_SUM_TYPE_COUNT] = {{1, "I"}, {4, "IV"}, {5, "V"}, {9, "IX"}, {10, "X"}, {40, "XL"}, {50, "L"}, {90, "XC"}, {100, "C"}, {400, "CD"}, {500, "D"},
        {900, "CM"}, {1000, "M"}};
    
    for (int i = ROMAN_SUM_TYPE_COUNT - 1; i >= 0; i--)
    {
        quotient = num/romanArray[i].interSum;
        while(quotient > 0)
        {
            strcat(answer, romanArray[i].romanStr);
            quotient--;
        }
        num = num % romanArray[i].interSum;
    }
    return answer;
}
```

还看到一些大神的简单做法：

```java
public static String intToRoman(int num) {
    String M[] = {"", "M", "MM", "MMM"};
    String C[] = {"", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"};
    String X[] = {"", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"};
    String I[] = {"", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"};
    return M[num/1000] + C[(num%1000)/100] + X[(num%100)/10] + I[num%10];
}
```

除了高喊nb，我还能说什么。