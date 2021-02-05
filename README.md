

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





## [剑指 Offer 10- I. 斐波那契数列](https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/)

+ 递归：不行。超时。

```java
class Solution {



    public int fib(int n) {


        
        if(n==0)
        {
            return 0;
        }
        else if(n==1)
        {
            return 1;
        }
        else{
            return (fib(n-1)+fib(n-2))%1000000007;
        }

        }

    }




```

+ 使用数组。

```java
class Solution {



    public int fib(int n) {
        
        if(n==0)
        {
            return 0;
        }

        if(n==1)
        {
            return 1;
        }

        int fi[]=new int [n+1];

        fi[0]=0;
        fi[1]=1;




        for(int i=2;i<n+1;i++)
        {
            fi[i]=fi[i-1]+fi[i-2];
            
            if(fi[i]>1000000007)
            {
                fi[i]=fi[i]%1000000007;
            }
            
        }
        return fi[n];



        }

    }




```

+ 为了保护数组需要在前面判断n=1和0时的情况。
+ 注意：为了防止溢出，需要在计算过程中就注意取模，而不只是在return处取模。

+ 官方题解：其实不需要数组，将其换成两个变量就够了。

 ```java
  class Solution {
  
  
  
      public int fib(int n) {
          
          if(n==0)
          {
              return 0;
          }
  
          if(n==1)
          {
              return 1;
          }
  
          //int fi[]=new int [n+1];
  
          int a=0;
          int b=1;
          int c=0;
  
  
  
  
          for(int i=1;i<n+1;i++)
          {
              
              
              if((a+b)>1000000007)
              {
                  c=(a+b)%1000000007;
              }
              else{
                  c=a+b;
              }
              
              b=a;
              a=c;
              
          }
          return c;
  
  
  
          }
  
      }
  
  
  
  
 ```

  

## [剑指 Offer 10- II. 青蛙跳台阶问题](https://leetcode-cn.com/problems/qing-wa-tiao-tai-jie-wen-ti-lcof/)

+ 同上

```java
class Solution {
    public int numWays(int n) {
        int a=0,b=0,c=0,count=1;
        if(n==0)
        {
            return 1; 
        }
        if(n==1)
        {
            return 1;
        }

        a=1;
        b=1;
        while(count<n)
        {
            if((a+b)>1000000007)
            {
                c=(a+b)%1000000007;
            }
            else
            {
            c=a+b;

            }
            a=b;
            b=c;
            count++;
        }
        return c;

    }
}
```



#### [剑指 Offer 12. 矩阵中的路径](https://leetcode-cn.com/problems/ju-zhen-zhong-de-lu-jing-lcof/)



tag:深度优先搜索

```java
class Solution {
    public boolean exist(char[][] board, String word) {
        char[] words = word.toCharArray();

        int x=0;
        int y=0;
        int count=0;
        int xboard=board.length;
        int yboard=board[0].length;
        while(x<xboard)
        {
            while(y<yboard)
            {
               
                if(dfs(x,y,words,count,board)==true)
                {
                    return true;
                }
                y++;
            }
            x++;
            y=0;
        }
        return false;
        

    
    }
    
        public boolean dfs(int x,int y,char[] words,int count,char[][] boardnew) {
                    
        int xboard=boardnew.length;
        int yboard=boardnew[0].length;
        boolean a,b,c,d=false;
   
        if(x<0||y<0||x==xboard||y==yboard)
        {
            return false;
        }
   


        if(words[count]==boardnew[x][y])
        {
            if(count==words.length-1)
            {
                return true;
            }
            else{
                boardnew[x][y]='!';
            // a=dfs(x+1,y,words,count+1,boardnew);
            // b=dfs(x-1,y,words,count+1,boardnew);
            // c=dfs(x,y+1,words,count+1,boardnew);
            // d=dfs(x,y-1,words,count+1,boardnew);
                

            if(dfs(x+1,y,words,count+1,boardnew)==true||dfs(x-1,y,words,count+1,boardnew)==true||dfs(x,y+1,words,count+1,boardnew)==true||dfs(x,y-1,words,count+1,boardnew)==true)
            {
                boardnew[x][y]=words[count];
                return true;
            }
            else{
                boardnew[x][y]=words[count];
                return false;
            }
            }
        }
        else
        {
            return false;
        }
        

        
        
    
    }



}
```

+ 建两个函数，一个作为主调用，一个作为dfs来递归。
+ “不走重复路”条件可以使用其它符号代替数组中该字符，本层递归后恢复；也可使用额外数组来记录。
+ 注意好边界的定义。
+ 注意可以使用｜｜（或）来减少时间上的浪费

#### [剑指 Offer 13. 机器人的运动范围](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/)

tag:深度优先搜索

```java
class Solution {
    int count=0;
    public int movingCount(int m, int n, int k) {
        int result=0;
        int[][] arrive=new int [m][n];
        

    
        for(int i=0;i<m;i++)
        {
            for (int j=0;j<n;j++)
            {
                if(dfs(i,j,k,m,n,0,0,arrive)==true)
                {
                    
                        result++;

                }
                

            }
        }
        return result;


        
        


    }

    boolean dfs(int aimx,int aimy,int k,int m, int n,int nowx,int nowy,int[][]arrive)
    {
        int nowx1=nowx/10;
        int nowx2=nowx%10;
        int nowy1=nowy/10;
        int nowy2=nowy%10;
        int sum=nowx1+nowx2+nowy1+nowy2;

        int aimx1=aimx/10;
        int aimx2=aimx%10;
        int aimy1=aimy/10;
        int aimy2=aimy%10;
        int sum1=aimx1+aimx2+aimy1+aimy2;

        if(sum1>k)
        {
            return false;
        }
        count++;
        if(count>1000000)
        {
            int aefsfefweaf=1;
        }




        if(sum>k||nowx==m||nowy==n||nowx==-1||nowy==-1||arrive[nowx][nowy]==1)
        {
            return false;
        }

        else if(nowx==aimx&&nowy==aimy)
        {
         return true;   
        }
          arrive[nowx][nowy]=1;

        if(dfs(aimx,aimy,k,m,n,nowx+1,nowy,arrive)||dfs(aimx,aimy,k,m,n,nowx-1,nowy,arrive)||dfs(aimx,aimy,k,m,n,nowx,nowy+1,arrive)||dfs(aimx,aimy,k,m,n,nowx,nowy-1,arrive))
        
        {
            arrive[nowx][nowy]=0;
            return true;
        }
        else
        {
            arrive[nowx][nowy]=0;
            return false;
        }



    }
}
```

爆栈了，复杂度过高。

```java
class Solution {
    int count=0;
    public int movingCount(int m, int n, int k) {
        int result=0;
        int[][] arrive=new int [m][n];
        


        return dfs(k,m,n,0,0,arrive);


        
        


    }

    int dfs(int k,int m, int n,int nowx,int nowy,int[][]arrive)
    {
        int nowx1=nowx/10;
        int nowx2=nowx%10;
        int nowy1=nowy/10;
        int nowy2=nowy%10;
        int sum=nowx1+nowx2+nowy1+nowy2;

        // int aimx1=aimx/10;
        // int aimx2=aimx%10;
        // int aimy1=aimy/10;
        // int aimy2=aimy%10;
        // int sum1=aimx1+aimx2+aimy1+aimy2;

        // if(sum1>k)
        // {
        //     return false;
        // }
        // count++;
        // if(count>1000000)
        // {
        //     int aefsfefweaf=1;
        // }




        if(sum>k||nowx==m||nowy==n||nowx==-1||nowy==-1||arrive[nowx][nowy]==1)
        {
            return 0;
        }

          arrive[nowx][nowy]=1;

        return dfs(k,m,n,nowx+1,nowy,arrive)+dfs(k,m,n,nowx-1,nowy,arrive)+dfs(k,m,n,nowx,nowy+1,arrive)+dfs(k,m,n,nowx,nowy-1,arrive)+1;
        



    }
}
```

绝了。

+ 方法一：多余。dfs是对的，不需要再次遍历每一个目标点以确认，造成极大的开销。

+ 在这种前后左右+1的深度搜索，就算有条件约束也可以遍历所有点。要充分信任。

+ 在记录数量的时候，可以使用

  ```java
  return dfs(k,m,n,nowx+1,nowy,arrive)+dfs(k,m,n,nowx-1,nowy,arrive)+dfs(k,m,n,nowx,nowy+1,arrive)+dfs(k,m,n,nowx,nowy-1,arrive)+1;
  ```

  的方法，很好用。






# [剑指 Offer 14- I. 剪绳子](https://leetcode-cn.com/problems/jian-sheng-zi-lcof/)

tag：深度优先搜索

法一 直接动态规划

```java
class Solution {
    public int cuttingRope(int n) {

        if(n==2||n==1||n==0)
    {
        return 1;
    }

int mark=0;
int m=n;
    for(int i=2;i<n;i++)
    {
            m=m-i;
            mark=Math.max(Math.max(i*cuttingRope(m),i*m),mark);
    }
    return mark;

    }
}

```

爆栈。暴力递归不可取，用数组记忆计算结果的方式。

```java
class Solution {
            int [] result=new int [58];
    public int cuttingRope(int n) {



        if(n==2||n==1||n==0)
    {
        return 1;
    }

        int mark=0;
        int m=n;


    for(int i=2;i<n;i++)
    {
            m=m-i;

           if(result[m]==0)
           {
            result[m]=cuttingRope(m);
            int b=Math.max(i*result[m],i*m);
            mark=Math.max(b,mark);

           }
           else
           {
                           int b=Math.max(i*result[m],i*m);
            mark=Math.max(b,mark);
           }





            m=m+i;
    }
    return mark;

    }
}


```

+ 数组记忆使用使用if语句判断，注意记忆递归的return值即可。
+ 注意有Math.max()方法。
+ 注意读题，题目要求从2开始。





```java
import java.math.BigInteger;

class Solution {
    int [] anser=new int [1000];
    public int cuttingRope(int n) {

        if(n<2)
            return 0;
        if(n==2)
            return 1;
            if(n==3)
            return 2;
        
        BigInteger[] dp = new BigInteger[n+1];
        dp[0]=new BigInteger("1");
        dp[1]=new BigInteger("1");
        dp[2]=new BigInteger("2");
        dp[3]=new BigInteger("3");



        for(int i=4;i<n+1;i++)
        {
            int p=n-i;
            // if(anser[p]==0)
            // {
            //     anser[p]=cuttingRope(p);
            //     result=Math.max(result,Math.max(anser[p]*i,i*p));
       
            // }

            // else
            // {
            // result=Math.max(result,Math.max(anser[p]*i,i*p));

            // }
            dp[i]=new BigInteger("0");
            for (int j=1;j<=i/2;j++)
            {
                dp[i]=dp[i].max(dp[j].multiply(dp[i-j]));
            }

        }

        return dp[n].mod(new BigInteger("1000000007")).intValue();
    }

    
}
```

