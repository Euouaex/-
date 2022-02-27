# -
算法个人理解
# 关于汉诺塔函数递归的自己的理解
个人在编写汉诺塔递归算法的时候，在网上找了很多教程，算法思想较为统一，属于是勉强看的懂，但是到了代码部分就看不明白了如下
***
    \\例如函数hanno为汉诺塔递归函数名
     hanno(n-1,A,C,B);
     printf("xxxxx");\\意为将第n个那个最大的盘子移到目标柱子上
     hanno(n-1,B,A,C);
***
对于其A,C,B柱子的分配，即使有文字叙述，但是仍不太明白ABC的转换方式，于是乎我将A,B,C三根柱子换了个叙述方式，换成**source**，**destination**，**temp**，意为源柱，目的柱子，以及辅助柱子，这样相对就比较清晰明了了

汉诺塔使用递归的思想本质即：若此时有n个盘子在**source**上，利用**temp**存放第n个最大盘子之前的n-1个盘子，而后将第n个处在**source**上的最大盘放到**destination**上，此时，**source**为空，**temp**上有n-1个盘子，**destination**上有1个盘子且为最大；这时我们的**destination**不变，即我们的目标柱子是不变的，但是我们可以把现在已经空置的**source**视为**temp**，即：将此时处在'=**temp**上的n-1个盘子中的n-2个移到**source**上面，此时**temp**中余下的最后一个（编号为n-1）相对于编号小于n-1的盘子中，最大的盘子，然后我们就可以把处在**temp**上的这个编号为n-1的盘子挪到**destination**上，完成第二个盘子的移动

以此类推，此时我们可以看到**source**上此时有n-2个盘子，**temp**上为0个，**destination**上为2个盘子，我们又可以回到上一段中提到的原始步骤，直到递归到只剩下一个盘子，其函数如下：
***
        void hanno(int n, char source, char destination, char temp)\\注意形参的含义和其对应位置
    {
        if (n == 1)
        {
            printf("将%c塔中的第%d个盘子移到%c上！\n", source, n, destination);
        }
        else
        {
            hanno(n - 1, source, temp, destination);
            printf("将%c塔中的第%d个盘子移到%c上！\n", source, n, destination);
            hanno(n - 1, temp, destination, source);
        }
    }
***
**函数参数n为本次操作时的盘子个数，*source*为本次操作的源柱子，*destination*为本次操作的目的柱子，*temp*为本次操作的辅助柱子。

在n为1时，函数直接打印结束，在不为1时，其依照刚刚所讲的形式进行递归，首先将n-1个盘子从**source**挪到**temp**上，所以此时需要用到**destination**作为辅助柱子

即**source**依旧为**source**，将**temp**视为**destination**，将**destination**视为**temp**，于是乎参数位置就如代码所示
***
     hanno(n - 1, source, temp, destination);
***
操作完成后，就将第n个处在**source**上的最大盘放到**destination**上
***
    printf("将%c塔中的第%d个盘子移到%c上！\n", source, n, destination);\\此时即打印：将源柱上的第n个盘子移到目的柱子上
***
接下来就是，把现在已经空置的**source**视为**temp**，将有n-1个盘子的**temp**视为**source**，**destination**不变
***
    hanno(n - 1, temp, destination, source);
***

---
我只能说，玩函数的形参和实参真有意思,说实话总体而言有那么点，宋丹丹老师的小品里面的，把大象装进冰箱需要几步，需要三步，第一步把门打开，第二部把大象装进去，第三步把门关上。
---
