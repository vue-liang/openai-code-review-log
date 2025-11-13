# 项目： OpenAi 代码评审.

### 😀代码评分：85
#### 😀代码逻辑与目的：
该代码包含了四个不同的Java类，分别针对不同的算法问题：数组旋转（Lc189）、最大子数组和（Lc53）、打家劫舍（Lc198）和买卖股票的最佳时机（Lc121）。每个类都包含一个主方法用于测试，以及一个或多个方法用于实现算法。

#### 🤔问题点：
1. **代码重复**：Lc189和Lc1891实现了相同的旋转数组功能，存在代码重复。
2. **命名规范**：类和方法命名不够清晰，例如`Lc189`和`Lc1891`。
3. **注释**：代码中缺少必要的注释，难以理解算法的实现细节。
4. **性能**：在Lc53中，使用数组来存储dp值可能不是最高效的，可以考虑使用变量来减少空间复杂度。
5. **边界条件**：在Lc189中，未对负数旋转次数进行特殊处理。

#### 🎯修改建议：
1. **移除重复代码**：删除Lc1891类，将Lc189中的代码复制到Lc1891中。
2. **改进命名规范**：将类名改为更具描述性的名称，例如`ArrayRotation`。
3. **添加注释**：在每个方法前添加注释，解释方法的用途和实现逻辑。
4. **优化Lc53**：使用变量代替数组来存储dp值。
5. **处理边界条件**：在Lc189中添加对负数旋转次数的处理。

#### 💻修改后的代码：
```java
// ArrayRotation.java
package com.liang.leetcode.array;

import java.util.Arrays;

public class ArrayRotation {
    public static void main(String[] args) {
        int[] nums = {1, 2, 3, 4, 5, 6, 7};
        rotate(nums, 3);
        System.out.println(Arrays.toString(nums));
    }

    public static void rotate(int[] nums, int k) {
        int len = nums.length;
        if (k == 0 || k == len || len <= 1) {
            return;
        }
        if (k < 0) {
            k = -k % len;
        }
        reverse(nums, 0, len - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, len - 1);
    }

    private static void reverse(int[] nums, int start, int end) {
        while (start < end) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }
}
```

```java
// MaxSubArray.java
package com.liang.leetcode.array;

public class MaxSubArray {
    public static void main(String[] args) {
        int[] nums = {-2, 1, -3, 4, -1, 2, 1, -5, 4};
        System.out.println(maxSubArray(nums));
    }

    public static int maxSubArray(int[] nums) {
        int pre = 0;
        int res = nums[0];
        for (int i = 1; i < nums.length; i++) {
            pre = Math.max(pre + nums[i], nums[i]);
            res = Math.max(res, pre);
        }
        return res;
    }
}
```

```java
// HouseRobber.java
package com.liang.leetcode.dp;

public class HouseRobber {
    public static void main(String[] args) {
        int[] nums = {1, 2, 3, 1};
        System.out.println(rob(nums));
    }

    public static int rob(int[] nums) {
        int len = nums.length;
        int[][] dp = new int[len][2];
        dp[0][0] = 0;
        dp[0][1] = nums[0];
        for (int i = 1; i < len; i++) {
            dp[i][0] = Math.max(dp[i - 1][1], dp[i - 1][0]);
            dp[i][1] = dp[i - 1][0] + nums[i];
        }
        return Math.max(dp[len - 1][1], dp[len - 1][0]);
    }
}
```

```java
// BestTimeToBuyAndSellStock.java
package com.liang.leetcode.greedy;

public class BestTimeToBuyAndSellStock {
    public static void main(String[] args) {
        int[] prices = {7, 1, 5, 3, 6, 4};
        System.out.println(maxProfit(prices));
    }

    private static int maxProfit(int[] prices) {
        int min = Integer.MAX_VALUE;
        int max = 0;
        for (int price : prices) {
            if (price < min) {
                min = price;
            } else if (price - min > max) {
                max = price - min;
            }
        }
        return max;
    }
}
```

#### 🌟代码中的优点：
- **算法正确性**：代码正确实现了各自的算法逻辑。
- **简单性**：代码结构简单，易于理解。