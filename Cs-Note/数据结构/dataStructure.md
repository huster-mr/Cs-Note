**题目描述：**
请实现一个函数，将一个字符串中的每个空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

**解题思路：**
先统计字符串的长度oldLen，同时也统计出空格的个数cnt，新字符串的长度为**oldLen+cnt*2**。采用一前一后两个指针，前面指向旧字符串的末尾，后面指向新字符串的末尾。然后从后往前遍历旧字符串， 遇到非空格字符时则拷贝到新字符串中即可，遇到空格时则在新字符串中添加“%20”。

**代码如下：**
**c++版本：**
```cpp
class Solution {
public:
	void replaceSpace(char *str,int length) {
        if(!str || length<1)
            return;
        int oldLen = 0;
        int cnt = 0;
        while(*str != '\0')
        {
            if(*str == ' ')
                ++cnt;
            ++oldLen;
            ++str;
        }
        int newLen = oldLen + cnt*2;
        if(newLen >= length)
            return;
        str[newLen+1] = '\0';
        while(newLen != oldLen)
        {
            if(str[oldLen] == ' ')
            {
                --oldLen;
                str[newLen--] = '0';
                str[newLen--] = '2';
                str[newLen--] = '%';
            }
            else
                str[newLen--] = str[oldLen--];
        }
        return;
	}
};
```

**Java版本：**
```java
public class Solution {
    public String replaceSpace(StringBuffer str) {
        int len = str.length();
        int spacenum = 0;
        for(int i=0; i<len; i++)
        {
            if(str.charAt(i) == ' ')
                spacenum++;
        }
        int newlen = len + spacenum*2;
        str.setLength(newlen);
        int indexOld = len-1;
        int indexNew = newlen-1;
        for(; indexOld>=0 && indexOld<indexNew; indexOld--)
        {
            if(str.charAt(indexOld) == ' ')
            {
                str.setCharAt(indexNew--, '0');
                str.setCharAt(indexNew--, '2');
                str.setCharAt(indexNew--, '%');
            }
            else
                str.setCharAt(indexNew--, str.charAt(indexOld));
        }
        return str.toString();
    }
}
```