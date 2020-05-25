# 每天一道leetCode

### 信息卡片

- 时间：2020-05-25
- 题目链接：https://leetcode-cn.com/problems/generate-parentheses
- tag：`递归` `深度优先` `广度优先` `DFS` `动态规划`

### 题目描述

```
数字 n 代表生成括号的对数，请你设计一个函数，用于能够生成所有可能的并且 有效的 括号组合。

 

示例：

输入：n = 3
输出：[
       "((()))",
       "(()())",
       "(())()",
       "()(())",
       "()()()"
     ]

```

### [参考答案](https://leetcode-cn.com/problems/generate-parentheses/solution/hui-su-suan-fa-by-liweiwei1419/)

#### 深度优先(DFS)
- 回溯 + 剪枝
- 判断条件：
- 前左右括号都有且大于 0 个可以使用的时候，才产生分支；
- 产生左分支的时候，只看当前是否还有左括号可以使用；
- 产生右分支的时候，还受到左分支的限制，右边剩余可以使用的括号数量一定得在严格大于左边剩余的数量的时候，才可以产生分支；
- 在左边和右边剩余的括号数都等于 0 的时候结算。

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<>();
        dfs("", n, n, result);
        return result;
    }

    private void dfs (String cur, int left, int right, List<String> result) {
        if (left == 0 && right == 0) {
            result.add(cur);
            return;
        }
        if (left > right) {
            return;
        }
        if (left > 0) {
            dfs(cur + "(", left - 1, right, result);
        }
        if (right > 0) {
            dfs(cur + ")", left, right - 1, result);
        }
    }
}
```

### 广度优先搜索
和深度优先搜索对比，感觉广度优先起码在这个题上不如深度优先搜索好用，首先需要编写结点类，代码更加复杂，其次时间上也不如深度优先快

```java

import java.util.ArrayDeque;
import java.util.ArrayList;
import java.util.Deque;
import java.util.LinkedList;
import java.util.List;
import java.util.Queue;

public class Solution {

    class Node {
        /**
         * 当前得到的字符串
         */
        private String res;
        /**
         * 剩余左括号数量
         */
        private int left;
        /**
         * 剩余右括号数量
         */
        private int right;

        public Node(String str, int left, int right) {
            this.res = str;
            this.left = left;
            this.right = right;
        }
    }

    public List<String> generateParenthesis(int n) {
        List<String> res = new ArrayList<>();
        if (n == 0) {
            return res;
        }
        Queue<Node> queue = new LinkedList<>();
        queue.offer(new Node("", n, n));

        while (!queue.isEmpty()) {

            Node curNode = queue.poll();
            if (curNode.left == 0 && curNode.right == 0) {
                res.add(curNode.res);
            }
            if (curNode.left > 0) {
                queue.offer(new Node(curNode.res + "(", curNode.left - 1, curNode.right));
            }
            if (curNode.right > 0 && curNode.left < curNode.right) {
                queue.offer(new Node(curNode.res + ")", curNode.left, curNode.right - 1));
            }
        }
        return res;
    }
}
```

### 动态规划
-
```java

```
