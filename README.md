# 2021-Coding-Interviews

###### 

### [剑指 Offer 04. 二维数组中的查找](https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)

+ error: reference binding to null pointer of type 'const value_type'

+ 原因：测试集为空

  > https://blog.csdn.net/wang13342322203/article/details/94323246

language:C++

TAG：树状数组 

```c++
class Solution {
public:
    bool findNumberIn2DArray(vector<vector<int>>& matrix, int target) {
        if (matrix.size()==0||matrix[0].size()==0)
        {
            return false;
        }
        else{
        int row=0,lie=matrix[0].size()-1;
            while(row<matrix.size()&lie>=0)
            {
                
                if(matrix[row][lie]>target)
                {
                    lie--;
                    continue;

                }
                else if (matrix[row][lie]<target)
                {
                    row++;
                    continue;
                }
                else{
                    return true;
                }
            }
            return false;
        }
    }
};
```

### [剑指 Offer 05. 替换空格](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/)

+ charAt() 方法用于返回指定索引处的字符

>runoob.com/java/java-string-charat.html

language:JAVA

TAG:字符串

```java
class Solution {
    public String replaceSpace(String s) {
             
        StringBuilder result = new StringBuilder();
        for(int i=0;i<s.length();i++)
        {
            char a=s.charAt(i);
            

            if (a==' ')
            {
                result.append("%20");
            }
            else
            {
                result.append(a);
            }



        }
        return result.toString();

    }
}
```

字符串的处理还是JAVA香.

### [剑指 Offer 06. 从尾到头打印链表](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

language:JAVA

TAG:链表

```java
/*
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public int[] reversePrint(ListNode head) {
        
        
        int count=0;
        ListNode countPoint=head;
        ListNode point=head;

        if(head==null)
        {
            int[] a=new int [0];
            return a;
        }
    
        if (countPoint!=null)
        {
            count=1;
        }

        while(countPoint.next!=null)
        {
            count++;
            countPoint=countPoint.next;

        }


        int[] data = new int[count];
        
        
        
        while(point!=null)
        {
            count=count-1;
            data[count]=point.val;
            point=point.next;
        }
        return data;

        

    }
}
```

注意判断链表为空的情况；

循环的终止条件注意是指针非空还是next非空。



