# 替换空格
+ https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/submissions/
## 解法1：利用java中的replace函数
```java
    // 
    // CharSequence对象先通过toString方法转化为String对象
    public String replaceSpace(String s) {
        return s.replace(" ","%20");
    }
 ```
 + 利用的是replace(CharSequence, CharSequence)函数,背后的实现是利用正则表达式对象Pattern.matcher()方法构造matcher对象, 再调用mathcer对象的replaceAll()方法
 + String对象中包含`private final char value[];`类型的成员变量，所以replace(char, char)的实现是基于这个value数组的 —— 先新建一个等长度数组，进行替换或赋值，返回一个利用替换之后的数组构建的新的String
 ```java
     public String replace(char oldChar, char newChar) {
        if (oldChar != newChar) {
            int len = value.length;
            int i = -1;
            char[] val = value; /* avoid getfield opcode */

            while (++i < len) {
                if (val[i] == oldChar) {
                    break;
                }
            }
            if (i < len) {
                char buf[] = new char[len];
                for (int j = 0; j < i; j++) {
                    buf[j] = val[j];
                }
                while (i < len) {
                    char c = val[i];
                    buf[i] = (c == oldChar) ? newChar : c;
                    i++;
                }
                return new String(buf, true);
            }
        }
        return this;
    }
 ```
 
 ## 解法2：从后向前替换,o(n)
 ```java   
    //从后往前，o(n)
    public String replaceSpace(String s) {
        char[] array = s.toCharArray();
        int countSpace = 0;
        for(int i = 0; i < array.length; i++){
            if(array[i] == ' ')
                countSpace++;
        }
        char[] newCharArray = new char[array.length + 2 * countSpace];//原题中char[]已预留好空间，所以在原数组上改
        int oldIdx = array.length - 1;
        int newIdx = newCharArray.length - 1;
        // System.out.println(oldIdx);
        while(oldIdx >= 0){
            // System.out.print(array[oldIdx]);
            if(array[oldIdx] != ' '){
                newCharArray[newIdx] = array[oldIdx];
                newIdx--;
                oldIdx--;
            }else{
                newCharArray[newIdx] = '0';
                newCharArray[newIdx-1] = '2';
                newCharArray[newIdx-2] = '%';
                newIdx -= 3;
                oldIdx--;
            }
        }
        return new String(newCharArray);
    }
```