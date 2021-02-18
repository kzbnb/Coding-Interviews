

# 2021-Coding-Interviews

## [剑指 Offer 04. 二维数组中的查找](https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)

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

## [剑指 Offer 05. 替换空格](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/)

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

## [剑指 Offer 06. 从尾到头打印链表](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

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

## [剑指 Offer 07. 重建二叉树](https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/)

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

### [面试题07. 重建二叉树（递归法，清晰图解）](https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/solution/mian-shi-ti-07-zhong-jian-er-cha-shu-di-gui-fa-qin/)

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



## [剑指 Offer 12. 矩阵中的路径](https://leetcode-cn.com/problems/ju-zhen-zhong-de-lu-jing-lcof/)



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

## [剑指 Offer 13. 机器人的运动范围](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/)

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






## [剑指 Offer 14- I. 剪绳子](https://leetcode-cn.com/problems/jian-sheng-zi-lcof/)

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



## [剑指 Offer 14- II. 剪绳子 II](https://leetcode-cn.com/problems/jian-sheng-zi-ii-lcof/)

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

+ BigInteger的使用和动态规划。

+ ```java
   for (int j=1;j<=i/2;j++)
              {
                  dp[i]=dp[i].max(dp[j].multiply(dp[i-j]));
              }
   ```


  ```

+ 经典动态规划

​```java
for (int i = 2; i <= n; i++) {
            for(int j=1;j<i;j++){
                int a = dp[i-j]*dp[j];
                int b = (i-j)*j;
                int c = dp[i-j]*j;
                int d = (i-j)*dp[j];
                int e = dp[i];
                dp[i] = max(a,b,c,d,e);
            }
        }
  ```

便于理解版本。

## [剑指 Offer 15. 二进制中1的个数](https://leetcode-cn.com/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/)

```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {

        int count=0;
        while(n!=0)
        
        {

            if((n&1)==1)
            {
                count++;
            }
            n>>>=1;
        }
        return count;
  
    }
}
```

注意，

>java提供两种右移运算符，属于位运算符。位运算符用来对二进制位进行操作。
>
>\>> ：算术右移运算符，也称带符号右移。用最高位填充移位后左侧的空位。
>
>\>>>：逻辑右移运算符，也称无符号右移。只对位进行操作，用0填充左侧的空位。





## [剑指 Offer 16. 数值的整数次方](https://leetcode-cn.com/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/)

tag：快速幂

```java
class Solution {
    public double myPow(double x, int n) {
            double result=1.0;
        if(x==0)
        {
            return 1;
        }

        long m=n;
        if(m<0)
        {
            x=1/x;
            m=-m;
        }
        while(m>0)
        {
            if(m%2==1)
            {
                m=m-1;
                result=result*x;
                x=x*x;
                m=m/2;

            }
            else
            {
           x=x*x;
                m=m/2;


            }
            
        }
return result;
        

    }
}



// if (power % 2 == 0) {
//             //如果指数为偶数
//             power = power / 2;//把指数缩小为一半
//             base = base * base % 1000;//底数变大成原来的平方
//         } else {
//             //如果指数为奇数
//             power = power - 1;//把指数减去1，使其变成一个偶数
//             result = result * base % 1000;//此时记得要把指数为奇数时分离出来的底数的一次方收集好
//             power = power / 2;//此时指数为偶数，可以继续执行操作
//             base = base * base % 1000;
//         }
```

+ 此题为快速幂。
+ https://blog.csdn.net/qq_19782019/article/details/85621386



## [剑指 Offer 17. 打印从1到最大的n位数](https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/)

```java
class Solution {
    public int[] printNumbers(int n) {
        int p=0;
        int count=1;
        while(n>0)
        {
            
            count=count*10;
            n=n-1;
        }
        int []result=new int [count-1];
        int num=0;
            while(count>1)
            {
                result[num]=num+1;
                num=num+1;
                count=count-1;
            }
            return result;
    }
}
```

据说原题是想考大数，leetcode没法运行。

https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/solution/mian-shi-ti-17-da-yin-cong-1-dao-zui-da-de-n-wei-2/



## [剑指 Offer 18. 删除链表的节点](https://leetcode-cn.com/problems/shan-chu-lian-biao-de-jie-dian-lcof/)

tag：链表

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode deleteNode(ListNode head, int val) {
        ListNode point=head;

         if(point.val==val)
            {
                return point.next;
            }

        while(point.next!=null)
        {
            
            if(point.next.val==val)
            {
                point.next=point.next.next;
            }
            else
            {
                point=point.next;
            }
        }

        return head;
        

    }
}
```

+ 链表头出现需要处理一下



## [剑指 Offer 21. 调整数组顺序使奇数位于偶数前面](https://leetcode-cn.com/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/)

+ 我的垃圾写法

```java
class Solution {
    public int[] exchange(int[] nums) {

            int[]num =new int [nums.length];
            int count=0;
            for(int i=0;i<nums.length;i++)
            {
                if(nums[i]%2==1)
                {
                    num[count]=nums[i];
                    count=count+1;
                }                
            }
                for(int i=0;i<nums.length;i++)
            {
                if(nums[i]%2==0)
                {
                    num[count]=nums[i];
                     count=count+1;

                }                
            }
            return num;




    }
}
```

快慢指针写法

```java
class Solution {
    public int[] exchange(int[] nums) {

            // int[]num =new int [nums.length];
            // int count=0;
            // for(int i=0;i<nums.length;i++)
            // {
            //     if(nums[i]%2==1)
            //     {
            //         num[count]=nums[i];
            //         count=count+1;
            //     }                
            // }
            //     for(int i=0;i<nums.length;i++)
            // {
            //     if(nums[i]%2==0)
            //     {
            //         num[count]=nums[i];
            //         count=count+1;

            //     }                
            // }
            // return num;

            int a=0,b=0;
            while(a!=nums.length&&b!=nums.length)
            {
                while(a<nums.length&&nums[a]%2==1)
                {//偶
                    a++;
                }
                    //奇
                    b++;
              

                if(a!=nums.length&&b!=nums.length&&nums[b]%2==1&&b>a)
                {
                int mid=nums[a];
                nums[a]=nums[b];
                nums[b]=mid;
                }



                
            }

return nums;




    }
}
```

+ 注意：快慢指针写法：两个while循环嵌套，一个在外+一个在里面+。

  tag：快慢指针

  

  首尾指针写法

  ```java
  class Solution {
      public int[] exchange(int[] nums) {
  
              // int[]num =new int [nums.length];
              // int count=0;
              // for(int i=0;i<nums.length;i++)
              // {
              //     if(nums[i]%2==1)
              //     {
              //         num[count]=nums[i];
              //         count=count+1;
              //     }                
              // }
              //     for(int i=0;i<nums.length;i++)
              // {
              //     if(nums[i]%2==0)
              //     {
              //         num[count]=nums[i];
              //         count=count+1;
  
              //     }                
              // }
              // return num;
  
  //             int a=0,b=0;
  //             while(a!=nums.length&&b!=nums.length)
  //             {
  //                 while(a<nums.length&&nums[a]%2==1)
  //                 {//偶
  //                     a++;
  //                 }
  //                     //奇
  //                     b++;
                
  
  //                 if(a!=nums.length&&b!=nums.length&&nums[b]%2==1&&b>a)
  //                 {
  //                 int mid=nums[a];
  //                 nums[a]=nums[b];
  //                 nums[b]=mid;
  //                 }
  
                  
  //             }
  
  // return nums;
  
  int a=0,b=nums.length-1;
  while(a<b)
  {
      while(a<nums.length&&nums[a]%2==1)
      {
              a=a+1;
              //偶
      }
      while(b>0&&nums[b]%2==0)
      {
          b=b-1;
      }
      if(a<b)
      {
      int mid=nums[a];
      nums[a]=nums[b];
      nums[b]=mid;
      }
  }
  return nums;
  
  
      }
  }
  ```

  + 注意边界判断

    tag：首尾指针

## [剑指 Offer 22. 链表中倒数第k个节点](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)

Tag:链表

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode getKthFromEnd(ListNode head, int k) {
        int count=0;
        ListNode headmark=head;
        if(headmark!=null)
        {
            count=1;
        }

        while(headmark.next!=null)
        {
        headmark=headmark.next;
        count=count+1;
        }
        headmark=head;
        int countting=0;

        while((k+countting)<count)
        {
        headmark=headmark.next;
        countting=countting+1;
        }
        return headmark;


    }
}
```

单指针方法，可行。

下面是只遍历一次的方法：

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode getKthFromEnd(ListNode head, int k) {
        // int count=0;
        // ListNode headmark=head;
        // if(headmark!=null)
        // {
        //     count=1;
        // }

        // while(headmark.next!=null)
        // {
        // headmark=headmark.next;
        // count=count+1;
        // }
        // headmark=head;
        // int countting=0;

        // while((k+countting)<count)
        // {
        // headmark=headmark.next;
        // countting=countting+1;
        // }
        // return headmark;

        int m=0;
        ListNode mark1=head,mark2=head;
            while(m<k&&mark1!=null)
            {
                mark1=mark1.next;
                m=m+1;

            }
            while(mark1!=null)
        {
            mark1=mark1.next;
            mark2=mark2.next;

        }

return mark2;



    }
}
```

## [剑指 Offer 24. 反转链表](https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof/)

+ 迭代的方法。

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
            ListNode cur=head;
            ListNode pre=null;
            ListNode next=null;

            if(head!=null&&head.next!=null)
            {
            next=head.next;
            }
            else
            {
              return head;
            }
          while(next!=null)
          {
            next=cur.next;
            cur.next=pre;
            pre=cur;
            if(next!=null)
            {
            cur=next;
            }

          }
          return cur;
            

          
    }
}
```

+ 递归的方法。

+ ```java
  /**
   * Definition for singly-linked list.
   * public class ListNode {
   *     int val;
   *     ListNode next;
   *     ListNode(int x) { val = x; }
   * }
   */
  class Solution {
      public ListNode reverseList(ListNode head) {
        if(head==null||head.next==null)
        {
          return head;
        }
             ListNode newhead=reverseList(head.next);
             head.next.next=head;
             head.next=null;
             return newhead;
             
      }
  }
  ```

  + 注意 head.next=null以保证原头结点不成loop。

## [剑指 Offer 25. 合并两个排序的链表](https://leetcode-cn.com/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/)

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode base=new ListNode(0);
        ListNode mark=base;
        
                while(l1!=null&&l2!=null)
                {
                    if(l1.val<l2.val)
                    {
                        
                        mark.next=l1;
                        l1=l1.next;

                    }
                    else
                    {
                        mark.next=l2;
                        l2=l2.next;
           
                    }
                    mark=mark.next;
                }


                if(l1==null)
                {
                    mark.next=l2;
                }
                else
                {
                    mark.next=l1;
                }

                return base.next;
         
    }
}
```

注意：

+ 输出的链表头的处理
+ 一条链表遍历到头后的处理
+ 注意new一个链表头

## [剑指 Offer 26. 树的子结构](https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof/)

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
  //先序遍历
    public boolean isSubStructure(TreeNode A, TreeNode B) {

            if(B==null||A==null)
            {
                return false;
            }

        return dfs(A,B)||isSubStructure(A.left,B)||isSubStructure(A.right,B);
            
    }

    boolean dfs(TreeNode A, TreeNode B)
    {
        if(A==null&&B==null)
        {
            return true;
        }
        else if(A==null)
        {
            return false;
        }
        else if (B==null)
        {
            return true;
        }
        else
        {
            if(A.val==B.val)
            {
                return dfs(A.left,B.left)&&dfs(A.right,B.right);
            }
            else
            {
                return false;
            }
        }
    }
}
```

关键点是边界的处理。

### [匹配类二叉树题目总结](https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof/solution/pi-pei-lei-er-cha-shu-ti-mu-zong-jie-by-z1m/)

## [剑指 Offer 27. 二叉树的镜像](https://leetcode-cn.com/problems/er-cha-shu-de-jing-xiang-lcof/)

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
    public TreeNode mirrorTree(TreeNode root) {

        if(root!=null)
        {
            TreeNode a=root.left;
            root.left=root.right;
            root.right=a;
            mirrorTree(root.left);
            mirrorTree(root.right);

        }
        return root;

    }
}
```

就这？

## [剑指 Offer 28. 对称的二叉树](https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/)

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
    public boolean isSymmetric(TreeNode root) {

        if(root==null)
        {
            return true;
        }
            else{
        return dfs(root.left,root.right);
            }

    }

    boolean dfs(TreeNode left,TreeNode right)
    {   
        if(left==null&&right==null)
        {
            return true;
        }
        else if(left==null||right==null)
        {
            return false;
        }
        if(left.val==right.val)
        {
            return dfs(left.left,right.right)&&dfs(left.right,right.left);
        }
        else
        {
            return false;
        }
    }

}
```

参照26题的思想。收藏大佬笔记：

> 做递归思考三步：
>
> 1. 递归的函数要干什么？
>
> - 函数的作用是判断传入的两个树是否镜像。
> - 输入：TreeNode left, TreeNode right
> - 输出：是：true，不是：false
>
> 1. 递归停止的条件是什么？
>
> - 左节点和右节点都为空 -> 倒底了都长得一样 ->true
> - 左节点为空的时候右节点不为空，或反之 -> 长得不一样-> false
> - 左右节点值不相等 -> 长得不一样 -> false
>
> 1. 从某层到下一层的关系是什么？
>
> - 要想两棵树镜像，那么一棵树左边的左边要和二棵树右边的右边镜像，一棵树左边的右边要和二棵树右边的左边镜像
> - 调用递归函数传入左左和右右
> - 调用递归函数传入左右和右左
> - 只有左左和右右镜像且左右和右左镜像的时候，我们才能说这两棵树是镜像的
>
> 1. 调用递归函数，我们想知道它的左右孩子是否镜像，传入的值是root的左孩子和右孩子。这之前记得判个root==null。

## [剑指 Offer 29. 顺时针打印矩阵](https://leetcode-cn.com/problems/shun-shi-zhen-da-yin-ju-zhen-lcof/)

```java
class Solution {
    public int[] spiralOrder(int[][] matrix) {
        int x=0,y=0,count=0;
        if(matrix.length==0)
        {
            return new int [0];
        }
        int you=matrix[0].length-1,xia=matrix.length-1,zuo=0,shang=0;
        
        int p=matrix.length*matrix[0].length;
        int []result=new int [p];
        

        while(count<p&&x>=0&&y>=0&&x<=matrix[0].length-1&&y<=matrix.length-1)
        {
            //左上
            x=zuo;
            y=shang;


            while(x<=you&&count<p)
            {
            result[count]=matrix[y][x];
            count++;
            x++;
            }

            //右上
            shang++;
            x=you;
            y=shang;

            while(y<=xia&&count<p)
            {
            result[count]=matrix[y][x];
            y++;
            count++;
            }

            //左下
            you--;
            x=you;
            y=xia;
           
            while(x>=zuo&&count<p)
            {
               
            result[count]=matrix[y][x];
            x--;
            count++;
            }

            //右下
            xia--;
            x=zuo;
            y=xia;
            
            while(y>=shang&&count<p)
            {
               
            result[count]=matrix[y][x];
            y--;
            count++;
            }
            zuo++;



           

            
        }
        return result;

    }
}
```

上面是自己的垃圾算法。

还可以大循环按圈走,小循环按边走。

## [剑指 Offer 30. 包含min函数的栈](https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/)

```java
class MinStack {
    Stack<Integer> A, B;

    /** initialize your data structure here. */
    public MinStack() {
            A=new Stack<>();
            B=new Stack<>();
    }
    
    public void push(int x) {

        A.push(x);
        if(!B.isEmpty()&&x<=B.peek())
        {
            B.push(x);
        }

        else if (B.isEmpty())
        {
            B.push(x);
        }

    }
    
    public void pop() {
                    int mark=A.pop();
                    if(mark==B.peek())
                    {
                    B.pop();
                    }
    }
    
    public int top() {
            return A.peek();
    }
    
    public int min() {
            return B.peek();
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.min();
 */
```

+ 思路是使用两个栈，一个栈实现正常功能，另一个实现min功能。

+ 一个栈的思路：判断现push元素是否小于min，若小于则push原min，然后push新min。

  

## [剑指 Offer 31. 栈的压入、弹出序列](https://leetcode-cn.com/problems/zhan-de-ya-ru-dan-chu-xu-lie-lcof/)

```java
class Solution {
    public boolean validateStackSequences(int[] pushed, int[] popped) {
        Deque<Integer> A = new LinkedList<>();
            int pu=0,po=0;
            while(pu<pushed.length)
            {
                if(pushed[pu]!=popped[po])
                {
                    A.push(pushed[pu]);
                    pu++;
                }
                else
                {
                    po++;
                    pu++;
                    
                    while(!A.isEmpty()&&po<popped.length&&A.peek()==popped[po])
                    {
                        po++;
                        A.pop();
                    }
                    
                    
                    
                    
                    
                    
                }
            }

            while(!A.isEmpty())
            {
                if(A.pop().equals(popped[po]))
                {
                    po++;
                }
            }

            if(po==popped.length)
            {
                return true;
            }
            else

            {
                return false;
            }

    }
}
```

+ 模拟法。注意判断能否连续pop出。

## [剑指 Offer 32 - I. 从上到下打印二叉树](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/)



tag：

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
    public int[] levelOrder(TreeNode root) {
        Queue<Integer> result=new LinkedList<>();
        Queue<TreeNode> waitingList=new LinkedList<TreeNode>();
        int count=0;

        if(root==null)
        {
            return new int [0];
        }
        waitingList.add(root);
        while(!waitingList.isEmpty())
        {
            TreeNode a=waitingList.poll();
            result.add(a.val);
            count++;
            if(a.left!=null)
            {
                waitingList.add(a.left);
            }
            if(a.right!=null)
            {
                waitingList.add(a.right);
            }
            

        }
        int [] asn=new int [count];
        int n=0;
        while(!result.isEmpty())
        {
                asn[n]=result.poll();
                n++;
        }
        return asn;
        
    }
}
```

+ 注意 BFS：使用Queue+一个while循环可以解决问题。

  



## [剑指 Offer 32 - II. 从上到下打印二叉树 II](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/)

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        Queue<TreeNode> waitingList =new LinkedList<>();
        Queue<Integer> result=new LinkedList<>();
        List<List<Integer>> an=new ArrayList();

        if(root==null)
        {
           return an;
        }
        int m=0;

        result.add(m);
        waitingList.add(root);
        
        while(!waitingList.isEmpty())
        {
            TreeNode a=waitingList.poll();
            int p=result.poll();
            if(p>an.size()-1)
            {
            an.add(new ArrayList());
            }
            an.get(p).add(a.val);
            m=p+1;
            if(a.left!=null)
            {
                result.add(m);
                waitingList.add(a.left);

            }   
            if(a.right!=null)
            {
                result.add(m);
                waitingList.add(a.right);



            }   

        }

        // List<List<Integer>> cancel=new ArrayList();
        // cancel.add(new ArrayList());
        // an.removeAll(cancel);

return an;




    }
}
```

+ 新增了层数的判断。使用变量标记。

+ LinkedList类实现了Queue接口，因此我们可以把LinkedList当成Queue来用。

+ 主要an.get()方法，可以得到第几个。

  > LinkedeList和ArrayList的区别
  >
  > 1、数据结构不同
  >
  > ArrayList是Array(动态数组)的数据结构，LinkedList是Link(链表)的数据结构。
  >
  > 2、效率不同
  >
  > 当随机访问List（get和set操作）时，ArrayList比LinkedList的效率更高，因为LinkedList是线性的数据存储方式，所以需要移动指针从前往后依次查找。
  >
  > 当对数据进行增加和删除的操作(add和remove操作)时，LinkedList比ArrayList的效率更高，因为ArrayList是数组，所以在其中进行增删操作时，会对操作点之后所有数据的下标索引造成影响，需要进行数据的移动。
  >
  > 3、自由性不同
  >
  > ArrayList自由性较低，因为它需要手动的设置固定大小的容量，但是它的使用比较方便，只需要创建，然后添加数据，通过调用下标进行使用；而LinkedList自由性较高，能够动态的随数据量的变化而变化，但是它不便于使用。
  >
  > 4、主要控件开销不同
  >
  > ArrayList主要控件开销在于需要在lList列表预留一定空间；而LinkList主要控件开销在于需要存储结点信息以及结点指针信息。



## [剑指 Offer 32 - III. 从上到下打印二叉树 III](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/)

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
    public List<List<Integer>> levelOrder(TreeNode root) {

            Queue<TreeNode>  wait =new LinkedList<>();
            List<List<Integer>> result=new LinkedList<>();
            int m=0;
            if(root==null)
            {
                return new LinkedList<>();
            }
            else
            {
                wait.add(new TreeNode(m));
                wait.add(root);
            }

            while(!wait.isEmpty())
            {
                int level=wait.poll().val;
                if(level>result.size()-1)
                {
                    result.add(new LinkedList<>());
                }
                TreeNode a=wait.poll();
                result.get(level).add(a.val);


               m=level+1;
                
                    if(a.left!=null)
                    {
                        wait.add(new TreeNode(m));
                        wait.add(a.left);
                    }
                    if(a.right!=null)
                    {
                        wait.add(new TreeNode(m));
                        wait.add(a.right);
                    }
                
                
            }

            for(int i=0;i<result.size();i++)
            {
                if(i%2==1)
                {
                    Collections.reverse(result.get(i));
                
                }
            }

            return result;




    }
}
```

 



在前面的例子里加上特定层数的反转。（辣鸡方法）

+ 注意

  ```java
  Collections.reverse(result.get(i));
  ```

  其中LinkedList实现了collections接口，可以这样用。

PS：

> Java接口和Java抽象类最大的一个区别，就在于Java抽象类可以提供某些方法的部分实现，而Java接口不可以**（就是interface中只能定义方法，而不能有方法的实现，而在abstract class中则可以既有方法的具体实现，又有没有具体实现的抽象方法）**
>
> Java接口是定义混合类型的理想工具，混合类表明一个类不仅仅具有某个主类型的行为，而且具有其他的次要行为。





+ 这个答案我觉得很好，多用一个队列，然后使用addLast和addFirst特性来做。

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        List<List<Integer>> res = new ArrayList<>();
        if(root != null) queue.add(root);
        while(!queue.isEmpty()) {
            LinkedList<Integer> tmp = new LinkedList<>();
            for(int i = queue.size(); i > 0; i--) {
                TreeNode node = queue.poll();
                if(res.size() % 2 == 0) tmp.addLast(node.val); // 偶数层 -> 队列头部
                else tmp.addFirst(node.val); // 奇数层 -> 队列尾部
                if(node.left != null) queue.add(node.left);
                if(node.right != null) queue.add(node.right);
            }
            res.add(tmp);
        }
        return res;
    }
}


```

## [剑指 Offer 33. 二叉搜索树的后序遍历序列](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/)

```java
class Solution {
    public boolean verifyPostorder(int[] postorder) {
        
        return helper(postorder,0,postorder.length-1);

    }

    boolean helper(int[] postorder,int start,int end)
    {

        if(!(start<end))
        {
            return true;
        }
        int small=start;
        while(postorder[small]<postorder[end])
        {
            small++;
        }
        int big=small;
        while(postorder[big]>postorder[end])
        {
            big++;
        }
        if(big==end)
        {
            
            return helper(postorder,start,small-1)&&helper(postorder,small,end-1);
        }
        else

        {
            return false;
        }


    }
}


```

+ 没做出来的主要原因是没认清二叉搜索树的定义（不是平衡的）。
+ 可以使用传数组+开始+结束下标的方式进行递归。



## [剑指 Offer 34. 二叉树中和为某一值的路径](https://leetcode-cn.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/)

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
            List<List<Integer>> result=new LinkedList<>();

    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<Integer> wait=new LinkedList<>();
        dfs(root,sum,wait);
        return result;

    }

       void dfs(TreeNode root, int sum,List<Integer> li)
     {
            if(root==null)
            {
                return;
            }
            List<Integer> lili=new LinkedList<>();
            lili.addAll(li);
            if(root.left==null&&root.right==null)
            {
                if(sum==root.val)
                {
                    lili.add(root.val);
                    result.add(lili);
                    return ;
                    
                }
                return ;
                
            }
            

            int val=root.val;
            int newSum=sum-val;
            lili.add(val);
            if(root.left!=null)
            {

                dfs(root.left,newSum,lili);
            }
            if(root.right!=null)
            {
                dfs(root.right,newSum,lili);
            }



     }
}
```

![image-20210214005048849](/Users/mac/Library/Application Support/typora-user-images/image-20210214005048849.png)

纪念一下，自己写的垃圾算法。

+  lili.addAll(li); 复制整个数组到新的数组可以用addAll()方法。

## [剑指 Offer 35. 复杂链表的复制](https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/)

```java
/*
// Definition for a Node.
class Node {
    int val;
    Node next;
    Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}
*/
class Solution {
    public Node copyRandomList(Node head) {
        if(head==null)
        {
            return null;
        }

        Map<Node,Node> map=new HashMap<>();
        Node point=head;
        


        while(point!=null)

        {
            
            map.put(point, new Node(point.val));
            
            point=point.next;
        }

        point=head;
        while(point!=null)
        {
            map.get(point).next=map.get(point.next);
            map.get(point).random=map.get(point.random);
            point=point.next;

        }
        return map.get(head);
        
    }
}
```

+ 注意hash的使用方法

+ ```java
  Map<Node, Node> map = new HashMap<>();
              map.put(point, new Node(point.val));
              map.get(point).next=map.get(point.next);
  
  ```

  https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/solution/jian-zhi-offer-35-fu-za-lian-biao-de-fu-zhi-ha-xi-/

  还有借用原链表，复制一份新链表+  .next，然后再拆开的办法。

## [剑指 Offer 36. 二叉搜索树与双向链表](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/)

+ 这题是关键是二叉搜索树的性质：中序遍历为保证由小到大。

+ 实现中序遍历，即把代码放中间，然后dfs递归。

+ 注意头尾的处理

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node left;
    public Node right;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val,Node _left,Node _right) {
        val = _val;
        left = _left;
        right = _right;
    }
};
*/
class Solution {
    Node pre,head;
    public Node treeToDoublyList(Node root) {
        if(root!=null)
        {
        dfs(root);


        }
        else
        {
            return null;
        }

        pre.right=head;
        head.left=pre;
        return head;

        
    }

    void dfs(Node cur)
    {
        
        if(cur==null)
        {
            return ;
        }
                int a=cur.val;

        dfs(cur.left);
        if(pre==null)
        {
            head=cur;
        }
        cur.left=pre;
        if(pre!=null)
        {
        pre.right=cur;
        }
        pre=cur;

        dfs(cur.right);
    }
}
```

## [剑指 Offer 38. 字符串的排列](https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/)

```java
class Solution {

    char[] pool;
    List<String> answer=new LinkedList<String>();
    public String[] permutation(String s) {
            pool=s.toCharArray();
            dfs(0);
            return answer.toArray(new String[answer.size()]);

    }

    void dfs(int x)
    {
        if(x==pool.length-1)
        {
            answer.add(String.valueOf(pool));///////////
        }
        HashSet set=new HashSet<>();
        for(int i=x;i<pool.length;i++)
        {
            if(set.contains(pool[i]))
            {
                continue ;
            }
            set.add(pool[i]);
            swap(i,x);
            dfs(x+1);
            swap(x,i);
        }
    }


    void swap(int a,int b)
    {
        char temp=pool[a];
        pool[a]=pool[b];
        pool[b]=temp;
    }
}
```

+ 在这用『换位』来表示各种组合。

+ String.toCharArray();

+ String.valueOf(pool)//将基本数据型态转换成 String

+ HashSet set=new HashSet<>();//该容器中只能存储不重复的对象。

+    void swap(int a,int b)
      {
          char temp=pool[a];
          pool[a]=pool[b];
          pool[b]=temp;
      }

  技巧有点多

## [剑指 Offer 39. 数组中出现次数超过一半的数字](https://leetcode-cn.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/)

```java
class Solution {
    public int majorityElement(int[] nums) {
            HashMap<Integer,Integer> map= new HashMap<>();
            int i=0;
            while(i<nums.length)
            {
                if(map.get(nums[i])==null)
                {
                    map.put(nums[i], 1);
                    
                }
                else
                {
                    int a=map.get(nums[i])+1;
                    if(a>nums.length/2)
                    {
                        return nums[i];
                    }
                    map.remove(nums[i]);
                    map.put(nums[i], a);
                }
                i++;
                
            }
            return nums[0];
            
    }
}
```

![image-20210216020720636](/Users/mac/Library/Application Support/typora-user-images/image-20210216020720636.png)

又费时间又费空间，我真牛逼

https://leetcode-cn.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/solution/mian-shi-ti-39-shu-zu-zhong-chu-xian-ci-shu-chao-3/

+ ！！！！众数问题可以用摩尔投票法！！！！

```java
class Solution {
    public int majorityElement(int[] nums) {
            //HashMap<Integer,Integer> map= new HashMap<>();
            // if(nums.length==1)
            // {
            //     return nums[0];
            // }
            int i=0;
            int voute=0;
            int z=nums[0];
            while(i<nums.length)
            {
                if(z!=nums[i])
                {
                    voute--;
                }
                else
                {
                    voute++;
                }
                if(voute==0)
                    {
                    z=nums[i];
                    }
                else
                {
                    i++;
                }
                    
            }
            return z;
            
    }
}
```

## [剑指 Offer 40. 最小的k个数](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/)

法一：快排。注意点很多

```java
class Solution {
    public int[] getLeastNumbers(int[] arr, int k) {
        qs(0,arr.length-1,arr);
            return Arrays.copyOf(arr, k);

    }




void qs(int zuo,int you,int []arr)
{
    if(zuo>=you)
    {
        return;
    }
    int origzuo=zuo,origyou=you;
    
    int base=arr[zuo];
    int nextbase=0;
    while (zuo < you){
            while (zuo < you && arr[you] >= base){
                you -- ;
            }
            while (zuo < you && arr[zuo] <= base){
                zuo ++ ;
            }
            swap(zuo,you,arr);
        }
        swap(origzuo,zuo,arr);
        nextbase=zuo;
        qs(origzuo,nextbase-1,arr);
        qs(nextbase+1,origyou,arr);


}

void swap(int one,int two,int []arr)
{
    int temp=arr[one];
    arr[one]=arr[two];
    arr[two]=temp;
}


}
```

+ 大循环嵌套俩小循环，大循环判断条件为俩哨兵相遇。
+ 注意若取最左的值为基准，则要右边先动。

原因：因为最终停下后，0号位需要放置一个小于baseline的数，而右边先动则保证了最终取出的数符合左👈🏻 边的规则，即小于baseline。

+ 注意在判断哨兵移动时需要取等号。
+ 每次都要判断两者有无相遇。
+ 主要保存原数组范围。

法二：大顶堆。

```java
class Solution {
    public int[] getLeastNumbers(int[] arr, int k) {
        if(k==0||arr==null)
        {
                return new int [0];
        }
        //List<Integer>result=new LinkedList<Integer>();
        int [] result=new int [k];
        PriorityQueue<Integer> dui=new PriorityQueue<>(k,new Comparator<Integer>()
        {
            //@override
            public int compare (Integer o1,Integer o2)
            {
                return o2-o1;
            }
            });
            int count=0;
        while(count<arr.length)
        {
            if(count<k)
            {
                dui.offer(arr[count]);
            }
            else
            {
                if(arr[count]<dui.peek())
                {
                    dui.poll();
                    dui.offer(arr[count]);
                }
            }
            count++;
        }
        count=0;
        while(!dui.isEmpty())
        {
                result[count]=dui.poll();
                count++;
        }
        return result;
        
        }
}

```

> https://blog.csdn.net/hefenglian/article/details/81807527

注意点也很多。

+ PriorityQueue默认为小顶堆，需要override Comparator，以传参的形式。或    PriorityQueue<Integer> dui=new PriorityQueue<>((r1,r2)->r2-r1);
+ PriorityQueued的add是offer

## [剑指 Offer 42. 连续子数组的最大和](https://leetcode-cn.com/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/)

```java
class Solution {
    public int maxSubArray(int[] nums) {
            // if(nums.length==0)
            // {
            //     return 0;
            // }
            int [] result=new int [nums.length];
            int count=0;
            
            result[count++]=nums[0];


            while(count<result.length)
            {
                if(result[count-1]<0)
                {
                    result[count]=nums[count];
                }
                else
                {
                    result[count]=nums[count]+result[count-1];
                }
                count++;
            }
            count=0;
            int max=Integer.MIN_VALUE;
            while(count<result.length)
            {
                if(result[count]>max)
                {
                    max=result[count];
                }
                count++;
            }
           return max;
            
    }
}
```

动态规划。

```java
class Solution {
    public int maxSubArray(int[] nums) {
            
            int count=1;

            while(count<nums.length)
            {
                if(nums[count-1]<0)
                {
                    nums[count]=nums[count];
                }
                else
                {
                    nums[count]=nums[count]+nums[count-1];
                }
                count++;
            }
            count=0;
            int max=Integer.MIN_VALUE;
            while(count<nums.length)
            {
                if(nums[count]>max)
                {
                    max=nums[count];
                }
                count++;
            }
           return max;
            
    }
}
```

不浪费空间版本。

## [剑指 Offer 44. 数字序列中某一位的数字](https://leetcode-cn.com/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/)

```java
class Solution {
    public int findNthDigit(int n) {
        //List<Character> save=new LinkedList<Character>();
       
        int counter=0;
        int count=1;
        int markp=0;

        while(count<n)
        {
            String a=String.valueOf(count);
            int p=0;
            while(p<a.length())
            {
                counter++;
                if(counter==n)
                {
                    markp=p;
                    break;
                }
                p++;
            }
            if(counter==n)
                {
                    break;
                }
            count++;
           
        }
        
        String a=String.valueOf(count);
        char p=a.charAt(markp);
        String stringc = String.valueOf(p);
        int sdaf=Integer.parseInt(stringc);
        



        return sdaf;
        
    }
}
```

```java
class Solution {
    public int findNthDigit(int n) {
        //List<Character> save=new LinkedList<Character>();
       
        int counter=0;
        int count=1;
        int markp=0;

        while(count<n)
        {
            String a=String.valueOf(count);
            

            if(counter>=997)
            {
                        int y=0;
            }
            counter=a.length()+counter;
            if(counter>n)
                {
                    markp=n-(counter-a.length())-1;
                    //count++;
                    
                    break;
                }
                else if(counter==n)
                {
                    markp=a.length()-1;
                    //count--;
                    break;
                }
            count++;
           
        }

        // while(counter<n)
        //     {
        //         counter++;
        //         markp++;

        //     }

        
        
        String a=String.valueOf(count);
        char p=a.charAt(markp);
        String stringc = String.valueOf(p);
        int sdaf=Integer.parseInt(stringc);
        



        return sdaf;
        
    }
}
```



思成的方法，爆时间了。

+ 注意后面取int某一位，需要 1.转String 2. 取char 3.转String 4.转Int

  同方法的StringBuilder版本

  ```java
  class Solution {
      public static int findNthDigit(int n) {
          StringBuilder s = new StringBuilder();
          int all = 0;
          for(int i = 0 ;all <= n ; i++){
              all += ((i / 10) + 1);
              s.append("" + i);
          }
          return Integer.parseInt(String.valueOf(s.charAt(n)));
      }
  }
  ```

  标注答案，傻逼题找规律

  ```java
  javaclass Solution {
      public int findNthDigit(int n) {
          int digit = 1;   // n所在数字的位数
          long start = 1;  // 数字范围开始的第一个数
          long count = 9;  // 占多少位
          while(n > count){
              n -= count;
              digit++;
              start *= 10;
              count = digit * start * 9;
          }
          long num = start + (n - 1) / digit;
          return Long.toString(num).charAt((n - 1) % digit) - '0';
      }
  }
  ```

  

## [剑指 Offer 45. 把数组排成最小的数](https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/)

```java
class Solution {
    public String minNumber(int[] nums) {
        StringBuilder res=new StringBuilder();
        Queue q=new PriorityQueue<String>(new Comparator<String>()
        {
            public int compare(String o1,String o2)

            {
                return (o1+o2).compareTo(o2+o1);
            }
        });
        int count=0;
        while(count<nums.length)
        {
            q.add(nums[count++]+"");

        }
        while(!q.isEmpty())
        {
            res.append(q.poll());
        }
        return res.toString();
    }
}




```

+ StringBuilder res=new StringBuilder(); 注意是append

+ 最关键的是，(o1+o2).compareTo(o2+o1)

+ ```java
   Queue q=new PriorityQueue<String>(new Comparator<String>()
          {
              public int compare(String o1,String o2)
    
              {
                  return (o1+o2).compareTo(o2+o1);
              }
          });
  ```

  小顶堆

## [剑指 Offer 46. 把数字翻译成字符串](https://leetcode-cn.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/)

```java
class Solution {
    public int translateNum(int num) {
        String snum=String.valueOf(num);
        char[] cnum=snum.toCharArray();
        int []dp=new int [cnum.length];
        dp[0]=1;
        //dp[1]=1;
        int count=1;
        

        while(count<cnum.length)
        {
            int b=Integer.parseInt(String.valueOf(cnum[count-1]));
            int c=Integer.parseInt(String.valueOf(cnum[count]));
            int a=b*10+c;
            dp[count]=dp[count-1];
            if(a<26&&a>9)
            {
                if(count==1)
                {
                    dp[1]=2;
                }
                else
                {
                    dp[count]=dp[count-1]+dp[count-2];
                }
            }
            else
            {
                if(count==1)
                {
                    dp[1]=1;
                }
            }
            count++;
        }
        return dp[cnum.length-1];
    }
}
```

动态规划。

+ b=Integer.parseInt(String.valueOf(cnum[count-1]));///char转int
+ 可以用滚动数组优化
+ 最重要的逻辑：*f*(*i*)=*f*(*i*−1)+*f*(*i*−2)



## 

## [剑指 Offer 47. 礼物的最大价值](https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof/)

```java
class Solution {
    public int maxValue(int[][] grid) {
            int m= grid.length ;
            int n=grid[0].length;
            int [][]res=new int [m][n];
           
            

            for(int i=0;i<m;i++)
            {
                for(int j=0;j<n;j++)
                {
                    int a=0,b=0;
                    if(i!=0)
                    {
                        a=res[i-1][j];
                      
                    }
                    if(j!=0)
                    {
                        b=res[i][j-1];
                    }
                        int p=grid[i][j];
                        
                        res[i][j]=Math.max(a, b)+p;
                        int q=res[i][j];
                        int wfweewf=q+1;
                    
                }
            }
            return res[m-1][n-1];
    }
}
```

动态规划，关键点在于一个点的最大值等于其上点或左点的最大值+本身值。 

+ 可只使用自己的原数组进行



## 

## [剑指 Offer 48. 最长不含重复字符的子字符串](https://leetcode-cn.com/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/)

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {


        
        int[] dp=new int [s.length()];
        int count=0;
        int trueRes=0;
        while(count<s.length())
        {
            int poi=count;
            int res=0;
            HashSet<Character> set=new HashSet<Character>();
            while(poi<s.length()&&!set.contains(s.charAt(poi)))
            {
                set.add(s.charAt(poi++));
                res++;
            }
            if(res>trueRes)
            {
                trueRes=res;
            }
            count++;
        }
        return trueRes;


    }
}
```

## [剑指 Offer 49. 丑数](https://leetcode-cn.com/problems/chou-shu-lcof/)

```java
class Solution {
    public int nthUglyNumber(int n) {
        Queue<Integer> min=new PriorityQueue<Integer>();
        //int []dp=new int [n];
        //dp[0]=1;
        // dp[1]=2;
        // dp[2]=3;
        // dp[3]=4;
        // dp[4]=5;
        
            for(int i=0;i<20;i++)
            {

                for(int m=0;m<40;m++)
                {
                    for(int p=0;p<40;p++)
                    {
                            double plus=Math.pow(2, p)*Math.pow(3, m)*Math.pow(5, i);

                            min.add((int)plus);
                    }
                }
            }
            int count=1;
            //min.poll();
            while(count<n)
            {
                //dp[count++]=min.poll();
                min.poll();
                count++;
            }
            return min.poll();


        

    }
}
```

这不炒？