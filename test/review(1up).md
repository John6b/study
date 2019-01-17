# 大一上软导复习简要
## 冒泡排序的伪代码

~~~
set swap to False
WHILE firstUnsorted<length-1
    FOR i FROM lastUnsorted to firstUnsorted+1
        IF list[i]<list[i-1]
        THEN set temp to list[i]
             set list[i] to list[i-1]
             set list[i-1] to list[i]
             set swap to True
        ENDIF
    ENDFOR
    IF swap==False
    THEN ENDWHILE
    ENDIF
    set firstUnsorted to firstUnsorted+1
    set swap to False
ENDWHILE
~~~

## Markdown 支持的 Latex 数学公式文本。
http://mohu.org/info/symbols/symbols.htm

![](..\images\mathnotation1.png)

![结果](..\images\mathnotation2.png)

![](..\images\mathnotation3.png)

![结果](..\images\mathnotation4.png)

## c语言位操作符号
非“~”，与“&”，或“|”，异或“^”

char c = 0xa1 & 0x70（用十六进制表示）；

 c = ( ？                )  
![答案为20（十六进制）](..\images\answer1.jpg)

### 请证明：二进制的负数（two‘s complement of X）等于 X 的 ones’ complement  ＋ 1（即，X每位求反加1）
![](..\images\proof1.jpg)

## 软件工程的概念

软件工程：
(1)将系统化、规范化、可度量的 方法应用与软件的开发、运行和维护的过程，即将工程化应用于软件中。
(2)对(1)中所述方法 的研究。——IEEE[IEE93]

##  软件生存周期
~~~
典型划分GB8567（4个时期7个阶段）： 
1）软件分析时期：问题定义、可行性研究、需求分析 
2）软件设计时期：总体设计、详细设计 
3）编码与测试时期：编码、测试 
4）运行与维护时期
~~~ 