

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