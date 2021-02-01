# 2021-Coding-Interviews

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



剑指offer答案：用栈或者递归

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

        if (head!=null)
        {
            count=1;
        }
        else 
        {
            int data[]=new int [0];
            return data;
        } 





 while(countPoint.next!=null)
        {
            count++;
            countPoint=countPoint.next;

        }
        countPoint=head;

        Stack<Integer> st = new Stack<Integer>();
		int data[] = new int[count]; /*开辟了一个长度为3的数组*/

        while(countPoint!=null)
        {
            st.push(countPoint.val);
            countPoint=countPoint.next;
        }
    int p=0;
        while(st.empty()!=true)
        {
            data[p]=st.pop();
            p++;
  
        }
return data;
        




        

    }
}
```

### [剑指 Offer 07. 重建二叉树](https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/)

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {


        HashMap<Integer,Integer> ma=new HashMap<>();
        
        for(int i=0;i<preorder.length;i++)
        {
            ma.put(inorder[i],i);
        }
        
        return rec(0,0,preorder.length-1,preorder,inorder,ma);



    }

    TreeNode rec(int root,int left,int right,int[] preorder,int[] inorder, HashMap<Integer,Integer> ma)
    {
        if(left>right)
        {
            return null;
        }

        TreeNode rootNode=new TreeNode(preorder[root]);
        int point=ma.get(preorder[root]);


        rootNode.left=rec(root+1,left,point-1,preorder,inorder,ma);
        rootNode.right=rec(root+point-left+1,point+1,right,preorder,inorder,ma);

        return rootNode;







    }



}
```

#### [面试题07. 重建二叉树（递归法，清晰图解）](https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/solution/mian-shi-ti-07-zhong-jian-er-cha-shu-di-gui-fa-qin/)

注意hashmap的创建方法和put、get。

注意root是前序中的顺序，其它是中序中的顺序。



## [剑指 Offer 11. 旋转数组的最小数字](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/)

```java
class Solution {
    public int minArray(int[] numbers) {

            int result=0;
            int low=0;
            int high=numbers.length-1;
            while(high>low)
            {
                int mid=(high+low)/2;
                if (numbers[high]>numbers[mid])
                {
                    high=mid;
                }
                else if(numbers[high]<numbers[mid])
                {
                    low=mid+1;
                }
                else
                {
                    high--;

                }

            }
            return numbers[low];


    }
}
```

+ 注意！mid=(high+low)/2; 由于取整数，导致mid有可能等于low导致死循环。因此当low=mid时，需要mid+1；
+ 注意当numbers[high]==numbers[mid]时，是high--，和low没关系。