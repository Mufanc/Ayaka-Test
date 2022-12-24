# Ayaka's Notes

<img src="./150px-Ayayaka.png" align="right" alt="Ayayaka"/>

## 依赖

* [`rust`](https://www.rust-lang.org/)：Ayaka CLI 使用 Rust 语言开发
* [`cargo`](https://crates.io/)：Rust 的构建系统和包管理器
* [`node.js`](https://nodejs.org/)：用于构建 Ayaka 前端
* [`pnpm`](https://pnpm.io/)：Node.js 的软件包管理器

## 食用方法

* 你说的对 ~~你说的对~~

### 二级-1

内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行行

#### 三级-1

<img style="width: 60%" src="./gjfrys.jpg" />

你说的对，但是《原神》是由米哈游自主研发的一款全新开放世界冒险游戏。游戏发生在一个被称作「提瓦特」的幻想世界，在这里，被神选中的人将被授予「神之眼」，导引元素之力‌​​​‌‌‌‌‌‌‌‌​​‌‌​‌‌‌​‌​。你将扮演一位名为「旅行者」的神秘角色，在自由的旅行中邂逅性格各异、能力独特的同伴们，和他们一起击败强敌，找回失散的亲人——同时，逐步发掘「原神」的真相。

#### 三级-2

```
<template>
    <main>
        <el-container>
            <div id="toc-box"></div>
            <el-main>
                <article class="py-1.5rem max-w-screen-md mx-auto prose">
                    <suspense>
                        <Markdown :src="path.join($route.path, 'index.md')" :extensions="[]" />
                    </suspense>
                </article>
            </el-main>
        </el-container>
    </main>
</template>
```

### 二级-2

* 🔨 从源码安装

```bash
git clone https://github.com/Mufanc/Ayaka && cd Ayaka
make install
代码长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长
高
高
高
高
高
高
高
高
高
高
高
高
高
高
高
高
高
高
高
高
高
```

* 🎉 在空文件夹中初始化 Ayaka

```bash
mkdir my-motes && cd my-notes
ayaka init
```

* 🆕 创建新文章

```bash
ayaka new <NAME>
```

* 🚀 生成单页应用（SPA）

```bash
ayaka gen
```

## 特性

- [ ] Todo

开新坑咯～

作为一名 NOIP 退役选手，已经两年（？）没有好好研究算法了，就连 CCF CSP 也全靠吃着高中的老本。~~然而做人如果没有梦想，那和一条咸鱼有什么分别呢？~~ 遂开此坑，有这时间去打原神每日，倒不如来 LeetCode 享受 A 题的快感（

有啥办法能自动更新文章标题么🤔，经常忘记改这玩意

## 2022 年 12 月 03 日

* [1796. 字符串中第二大的数字](https://leetcode.cn/problems/second-largest-digit-in-a-string/)｜难度：{% span green, 简单 %}

### 解题思路长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长

500 个点直接排序……应该也不算慢吧🤔

```rust
impl Solution {
    pub fn second_highest(str: String) -> i32 {
        let mut digits: Vec<_> = str
            .chars()
            .filter(|it| it.is_ascii_digit())
            .map(|it| it as i32 - 0x30)
            .collect();
        digits.sort_by_key(|it| -it);
        digits.dedup();
        if let Some(ans) = digits.get(1) {
            *ans
        } else {
            -1
        }
    }
}

```

## 2022 年 12 月 02 日

* [1769. 移动所有球到每个盒子所需的最小操作数](https://leetcode.cn/problems/minimum-number-of-operations-to-move-all-balls-to-each-box/)｜难度：{% span blue, 中等 %}

### 解题思路

这是一个暴力解。对于每个位置，统计所有「1」到它的距离之和：

```rust
impl Solution {
    pub fn min_operations(boxes: String) -> Vec<i32> {
        let ones: Vec<_> = boxes
            .chars()
            .enumerate()
            .filter(|it| it.1 == '1')
            .map(|it| it.0 as i32)
            .collect();
        (0..boxes.len() as i32)
            .map(|it| ones.iter().map(|x| (it - x).abs()).sum())
            .collect()
    }
}

```

遍历数组，同时维护指针两侧 1 的数量，可以达到 $O(n)$（但是懒得写了

## 2022 年 12 月 01 日

* [1779. 找到最近的有相同 X 或 Y 坐标的点](https://leetcode.cn/problems/find-nearest-point-that-has-the-same-x-or-y-coordinate/)｜难度：{% span green, 简单 %}

### 解题思路

先找出所有有效的点，然后取最小值

```rust
impl Solution {
    pub fn nearest_valid_point(x: i32, y: i32, points: Vec<Vec<i32>>) -> i32 {
        let mut valid = vec![];
        for (index, xy) in points.into_iter().enumerate() {
            if x == xy[0] || y == xy[1] {
                valid.push(((x - xy[0]).abs() + (y - xy[1]).abs(), index as i32));
            }
        }
        if valid.is_empty() {
            -1
        } else {
            valid.into_iter().min().unwrap().1
        }
    }
}
```

## 2022 年 11 月 30 日

* [895. 最大频率栈](https://leetcode.cn/problems/maximum-frequency-stack/)｜难度：{% span red, 困难 %}

### 解题思路

没思路，把题解翻译成 Rust 的交了（

```rust
use std::cmp;
use std::collections::HashMap;

struct FreqStack {
    freq: HashMap<i32, i32>,
    group: HashMap<i32, Vec<i32>>,
    max: i32
}

impl FreqStack {
    fn new() -> Self {
        Self {
            freq: HashMap::new(),
            group: HashMap::new(),
            max: 0
        }
    }

    fn push(&mut self, val: i32) {
        self.freq.entry(val).and_modify(|it| *it += 1).or_insert(0);
        self.group.entry(self.freq[&val]).and_modify(|it| it.push(val)).or_insert(vec![val]);
        self.max = cmp::max(self.max, self.freq[&val]);
    }

    fn pop(&mut self) -> i32 {
        let val = self.group.get_mut(&self.max).and_then(|it| it.pop()).unwrap();
        self.freq.entry(val).and_modify(|it| *it -= 1);
        if self.group[&self.max].is_empty() {
            self.max -= 1;
        }
        val
    }
}

```

## 2022 年 11 月 29 日

* [1758. 生成交替二进制字符串的最少操作数](https://leetcode.cn/problems/minimum-changes-to-make-alternating-binary-string/)｜难度：{% span green, 简单 %}

### 解题思路

简单题，直接上代码

```rust
use std::cmp::min;

impl Solution {
    pub fn min_operations(str: String) -> i32 {
        let (mut a, mut b) = (0, 0);

        for (i, ch) in str.chars().enumerate() {
            let ch = ch as usize - '0' as usize;
            if i & 1 != ch { a += 1 }
            if i & 1 == ch { b += 1 }
        }

        min(a, b)
    }
}
```

## 2022 年 11 月 28 日

* [813. 最大平均值和的分组](https://leetcode.cn/problems/largest-sum-of-averages/)｜难度：{% span blue, 中等 %}

### 解题思路

记忆化搜索，`search(n, k)` 表示前 n 个元素分成 k 个子数组的最大平均和，遍历分隔点，与 `search(i, k - 1)` 相加取最大值：

```rust
struct Cache {
    memory: Vec<Vec<f64>>,
}

impl Cache {
    fn new(n: usize) -> Self {
        Self {
            memory: vec![vec![-1.; n]; n],
        }
    }

    fn search(&mut self, sums: &[f64], n: usize, k: usize) -> f64 {
        if k == 1 {
            return sums[n] / n as f64
        }
        match self.memory[n][k] {
            it if it > 0. => it,
            _ => {
                let mut ans = -1.;
                for i in k - 1 .. n {
                    ans = f64::max(
                        ans,
                        self.search(sums, i, k - 1) + (sums[n] - sums[i]) / (n - i) as f64,
                    );
                }
                self.memory[n][k] = ans;
                ans
            }
        }
    }
}

impl Solution {
    pub fn largest_sum_of_averages(nums: Vec<i32>, k: i32) -> f64 {
        let (n, k) = (nums.len(), k as usize);

        let mut sums = vec![0.];
        for it in nums {
            sums.push(sums.last().unwrap() + it as f64);
        }


        Cache::new(n + 1).search(&sums, n, k)
    }
}

```

## 2022 年 11 月 27 日

* [1752. 检查数组是否经排序和轮转得到](https://leetcode.cn/problems/check-if-array-is-sorted-and-rotated/)｜难度：{% span green, 简单 %}

### 解题思路

符合条件的数组在「循环轮转」过程中应至多只有一次下跌：

```rust
impl Solution {
    pub fn check(mut nums: Vec<i32>) -> bool {
        nums.push(nums[0]);
        let result =
            nums.into_iter().fold(
                (0, 0),
                |(pre, sum), it| {
                    if pre > it {
                        (it, sum + 1)
                    } else {
                        (it, sum)
                    }
                },
            );
        result.1 < 2
    }
}
```

## 2022 年 11 月 26 日

* [882. 细分图中的可到达节点](https://leetcode.cn/problems/reachable-nodes-in-subdivided-graph/)｜难度：{% span red, 困难 %}

### 解题思路

细分后的节点数其实就是某种意义上的边权，可以在 Dijkstra 算法的基础之上加以改进来完成本题，具体操作见代码：

```rust
use std::cmp::Ordering;
use std::collections::{BinaryHeap, HashMap};

#[derive(Eq)]  // BinaryHeap 用
struct Task {  //  Dijkstra - 优先队列的任务类
    node: usize,
    distance: u32,
}

impl Ord for Task {  // BinaryHeap 用
    fn cmp(&self, other: &Self) -> Ordering {
        other.distance.cmp(&self.distance)
    }
}

impl PartialOrd for Task {  // BinaryHeap 用
    fn partial_cmp(&self, other: &Self) -> Option<Ordering> {
        Some(self.cmp(other))
    }
}

impl PartialEq for Task {  // BinaryHeap 用
    fn eq(&self, other: &Self) -> bool {
        self.distance == other.distance
    }
}

impl Task {
    fn new(node: usize, distance: u32) -> Self {
        Self { node, distance }
    }
}

impl Solution {
    pub fn reachable_nodes(edges: Vec<Vec<i32>>, max_moves: i32, n: i32) -> i32 {
        let (n, max_moves) = (n as usize, max_moves as u32);  // 预处理：类型转换

        let mut graph: HashMap<usize, HashMap<usize, u32>> = HashMap::new();  // 存图：当前节点 -> 下一节点 -> 边权

        for next in edges {  // 建图
            for index in 0 ..= 1 {
                let (src, dst) = (next[index] as usize, next[1 - index] as usize);
                let distance = next[2] as u32 + 1;

                graph
                    .entry(src)
                    .and_modify(|map| {
                        map.insert(dst, distance);
                    })
                    .or_insert(HashMap::from([(dst, distance)]));
            }
        }

        let mut distance = vec![u32::MAX; n];
        let mut visit = vec![false; n];
        let mut queue: BinaryHeap<Task> = BinaryHeap::new();

        distance[0] = 0;
        queue.push(Task::new(0, 0));

        while let Some(Task { node: src, .. }) = queue.pop() {  // Dijkstra
            if visit[src] { continue; }
            visit[src] = true;

            if !graph.contains_key(&src) {
                continue;
            }

            for (dst, range) in &graph[&src] {
                let new_distance = distance[src] + range;

                if distance[*dst] > new_distance {
                    distance[*dst] = new_distance;
                    queue.push(Task::new(*dst, new_distance));
                }
            }
        }

        let mut ans = 0;

        for it in &mut visit {
            *it = false;
        }

        for (src, moves) in distance.iter().enumerate() {
            if *moves > max_moves { continue; }  // 如果该节点不可达，则直接返回

            ans += 1;  // 统计初始节点
            visit[src] = true;

            if !graph.contains_key(&src) {
                continue;
            }

            for (dst, range) in &graph[&src] {  // 统计扩展节点
                if !visit[*dst] {
                    ans += (max_moves.saturating_sub(*moves)
                        + max_moves.saturating_sub(distance[*dst]))
                    .min(*range - 1);
                }
            }
        }

        ans as i32
    }
}
```

## 2022 年 11 月 25 日

* [809. 情感丰富的文字](https://leetcode.cn/problems/expressive-words/)｜难度：{% span blue, 中等 %}

### 解题思路

将所有单词拆分成「字母 - 长度」序列，例如 `hello` 可处理成 `[(h, 1), (e, 1), (l, 2), (o, 1)]`，然后就可以很容易地判断每个输入是否满足条件。一个满足条件的单词 word 应符合：

* word 与 str 拆分后序列长度相同

* 对应位置上的字符相等

* 对应位置字符的数量相等；或来自 str 的字符数大于等于 3，且大于来着 word 的字符数

基于此，可以编写代码：

```rust
impl Solution {
    fn split(str: String) -> Vec<(char, usize)> {
        let mut result: Vec<(char, usize)> = vec![];
        for ch in str.chars() {
            match result.last_mut() {
                Some(it) if it.0 == ch => it.1 += 1,
                _ => result.push((ch, 1)),
            }
        }
        result
    }

    pub fn expressive_words(str: String, words: Vec<String>) -> i32 {
        let str = Self::split(str);

        let mut ans = 0;

        for word in words {
            let word = Self::split(word);
            if word.len() != str.len() {
                continue;
            }
            if str
                .iter()
                .zip(word)
                .all(|(x, y)| x.0 == y.0 && (x.1 == y.1 || x.1 >= 3.max(y.1)))
            {
                ans += 1;
            }
        }

        ans
    }
}
```

## 2022 年 11 月 24 日

* [795. 区间子数组个数](https://leetcode.cn/problems/number-of-subarrays-with-bounded-maximum/)｜难度：{% span blue, 中等 %}

### 解题思路

将数字分为大、中、小三类，其中「中数」指的是落在区间 $[L, R]$ 中的数。按区间划分数组，显然长度为 $k$ 的区间的子区间数量为 $\frac{k^2 + k}{2}$，分别计算「中数」和「小数」的区间对答案的贡献（注意「小数」区间是负贡献），求和之后即为最终答案：

```rust
impl Solution {
    pub fn num_subarray_bounded_max(mut nums: Vec<i32>, left: i32, right: i32) -> i32 {
        nums.push(i32::MAX);  // 便于计算最后一个区间

        let mut ans: i64 = 0;
        let (mut mid, mut min) = (0, 0);

        for i in 0 .. nums.len() {
            if nums[i] > right {  // 区间结束，结算「中数」
                let n = (i - mid) as i64;
                ans += (n * (n + 1)) / 2;
                mid = i + 1;
            }
            if nums[i] >= left {  // 区间结束，结算「小数」
                let n = (i - min) as i64;
                ans -= (n * (n + 1)) / 2;
                min = i + 1;
            }
        }

        ans as i32
    }
}
```

## 2022 年 11 月 23 日

* [1742. 盒子中小球的最大数量](https://leetcode.cn/problems/maximum-number-of-balls-in-a-box/)｜难度：{% span green, 简单 %}

### 解题思路

模拟，按题目要求统计数量后取最大值：

```rust
use std::collections::HashMap;

impl Solution {
    pub fn count_balls(low_limit: i32, high_limit: i32) -> i32 {
        let mut map = HashMap::new();

        for mut it in low_limit ..= high_limit {
            let mut sum = 0;
            while it != 0 {
                sum += it % 10;
                it /= 10;
            }
            if let Some(val) = map.remove(&sum) {
                map.insert(sum, val + 1);
            } else {
                map.insert(sum, 1);
            }
        }

        *map.values().max().unwrap()
    }
}
```

## 2022 年 11 月 22 日

* [878. 第 N 个神奇数字](https://leetcode.cn/problems/nth-magical-number/)｜难度：{% span red, 困难 %}

### 解题思路

设第 n 个「神奇数字」为 x，不难发现随着 n 的增长，x 的变化呈现周期性，其周期为：

$$
T = \frac{\text{lcm}(a, b)}{a} + \frac{\text{lcm}(a, b)}{b} - 1 = \frac{a}{\text{gcd}(a, b)} + \frac{b}{\text{gcd}(a, b)} - 1
$$

$T$ 与 a、b 同一数量级，我们可以快速求出前面整数个周期的 x 值，然后暴力求解剩余部分（似乎可以二分？）：

```rust
const MOD: u64 = 1_000_000_007;

fn gcd(a: u64, b: u64) -> u64 {
    if a < b {
        return gcd(b, a);
    }
    if b == 0 {
        return a;
    }
    gcd(b, a % b)
}

impl Solution {
    pub fn nth_magical_number(n: i32, a: i32, b: i32) -> i32 {
        let (n, a, b) = (n as u64, a as u64, b as u64);

        let gcd = gcd(a, b);
        let lcm = a * b / gcd;
        let cycle = a / gcd + b / gcd - 1;

        let base = n / cycle * lcm % MOD;

        let (mut last, mut ax, mut bx) = (0, a, b);
        for _ in 0 .. n % cycle {
            if ax < bx {
                last = ax;
                ax += a;
            } else {
                last = bx;
                bx += b;
            }
        }

        ((base + last) % MOD) as _
    }
}
```

时间复杂度 $O(\log \text{max}(a, b) + \text{max}(a, b))$

## 2022 年 11 月 21 日

* [808. 分汤](https://leetcode.cn/problems/soup-servings/)｜难度：{% span blue, 中等 %}

### 解题思路

被题目的 `n < 1e9` 骗了，想了很久都没找到小于 $O(n^2)$ 的解法，后来发现在题目给定的精度下，只要 n 大于一定值（约为 5000）就可以直接返回 1

另外不难注意到，可以将 n 向上取整到 25 的倍数来进一步减小常数，最终只需要做一个 $O(- \log k)$ 级别（$k$ 为精度，本题中 $k = 10^{-5}$）的记忆化搜索就可以了

```rust
use std::collections::HashMap;

#[derive(Default)]
struct Cache {
    cache: HashMap<(i32, i32), f64>
}

impl Cache {
    fn search(&mut self, a: i32, b: i32) -> f64 {  // 记忆化搜索
        if self.cache.contains_key(&(a, b)) {
            return self.cache[&(a, b)];
        }

        let result = match (a, b) {
            (a, b) if (a <= 0 && b <= 0) => 0. + 0.5,  // 同时分配完
            (a, _) if (a <= 0) => 1. + 0.,  // A 先分配完
            (_, b) if (b <= 0) => 0. + 0.,  // B 先分配完
            (a, b) => {
                (0 .. 4).map(|i| self.search(a - 4 + i, b - i)).sum::<f64>() * 0.25
            }
        };

        self.cache.insert((a, b), result);
        result
    }
}

impl Solution {
    pub fn soup_servings(mut n: i32) -> f64 {
        n = (n + 24) / 25;  // 向上取整至 25 的整数倍 + 归一化

        if n >= 200 {
            return 1.;
        }

        Cache::default().search(n, n)
    }
}
```

## 2022 年 11 月 20 日

* [799. 香槟塔](https://leetcode.cn/problems/champagne-tower/)｜难度：{% span blue, 中等 %}

### 解题思路

一杯一杯地倒和一次全倒完是一样的，我们可以把所有香槟都先倒在 `[0, 0]` 杯子里，然后向下处理溢出：

```rust
impl Solution {
    pub fn champagne_tower(poured: i32, row: i32, index: i32) -> f64 {
        let (poured, row, index) = (poured as f64, row as usize, index as usize);

        let mut dp = vec![vec![0.; row + 2]; row + 2];
        dp[0][0] = poured;

        for i in 0 ..= row {
            for j in 0 ..= i {
                if dp[i][j] > 1. {
                    let overflow = (dp[i][j] - 1.) / 2.;
                    dp[i + 1][j] += overflow;
                    dp[i + 1][j + 1] += overflow;
                    dp[i][j] = 1.;
                }
            }
        }

        dp[row][index]
    }
}

```

时间和空间都还能做一些优化，懒得搞了。以及似乎有数学解法（？

## 2022 年 11 月 19 日

* [1732. 找到最高海拔](https://leetcode.cn/problems/find-the-highest-altitude/)｜难度：{% span green, 简单 %}

### 解题思路

求前缀和，然后找最大值即可

```rust
impl Solution {
    pub fn largest_altitude(gain: Vec<i32>) -> i32 {
        let mut alt = vec![0];

        for it in gain {
            alt.push(alt.last().unwrap() + it);
        }

        *alt.iter().max().unwrap()
    }
}
```

## 2022 年 11 月 18 日

* [891. 子序列宽度之和](https://leetcode.cn/problems/sum-of-subsequence-widths/)｜难度：{% span red, 困难 %}

### 解题思路

考虑一段跨度为 $k$ （首尾元素下标之差为 $k-1$）的子序列 $S$ 对宽度和的贡献值：

$$
W = (\max(S) - \min(S)) \cdot 2^{k - 2}
$$

其中 $\max(S) - \min(S)$ 为贡献值， $2^{k - 2}$ 是跨度为 $k$ 的字序列数量（即两头元素必取，中间任意选择）。不难看出数组如何排序并不会影响最终结果，所以我们可以先将数组按照升序排序，便于后续的处理，此时数组整体的宽度和可表示为：

$$
\begin{align*}
W_{\sum} &= \sum_{i = 1}^{N - 1} \sum_{j = 0}^{i - 1} (a_i - a_j) \cdot 2^{i - j - 1} \\
  &= \sum_{i = 1}^{N - 1}(a_i \cdot \sum_{j = 0}^{i - 1} 2^{i - j - 1} - \sum_{j = 0}^{i - 1} a_j \cdot 2^{i - j - 1}) \\
  &= \sum_{i = 1}^{N - 1} a_i \cdot (2^i - 1) - \sum_{i = 1}^{N - 1} \sum_{j = 0}^{i - 1} a_j \cdot 2^{i - j - 1} \\
  &= \sum_{i = 1}^{N - 1} a_i \cdot (2^i - 1) - \sum_{j = 0}^{N - 2} a_j \cdot \sum_{i = j + 1}^{N - 1} 2^{i - j - 1} \\
  &= \sum_{i = 1}^{N - 1} a_i \cdot (2^i - 1) - \sum_{j = 0}^{N - 2} a_j \cdot (2^{N - j - 1} - 1) \\
  &= \sum_{k = 1}^{N - 1} \left[ a_k \cdot (2^k - 1) - a_{k - 1} \cdot (2^{N - k} - 1) \right]
\end{align*}
$$

利用等比数列的求和公式，我们巧妙地把 $O(n^2)$ 复杂度的双重循环降低到只有一重循环，此外还注意到，我们可以在 $O(n)$ 时间复杂度内递推处理出所有的 $2^k$ 的值，所以最终时间复杂度只有 $O(n)$

```rust
const MOD: u64 = 1000000007;

impl Solution {
    pub fn sum_subseq_widths(nums: Vec<i32>) -> i32 {
        let n = nums.len();
        let mut nums: Vec<_> = nums.into_iter().map(|it| it as u64).collect();
        nums.sort();

        let mut ans = 0;
        let mut pow_k = vec![1];

        for i in 1 .. n {
            pow_k.push(pow_k[i - 1] * 2 % MOD);
        }

        for i in 1 .. n {
            ans += (nums[i] * (pow_k[i] - 1)) % MOD;
            ans += MOD - (nums[i - 1] * (pow_k[n - i] - 1)) % MOD;
            ans %= MOD;
        }

        ans as _
    }
}
```

## 2022 年 11 月 17 日

* [792. 匹配子序列的单词数](https://leetcode.cn/problems/number-of-matching-subsequences/)｜难度：{% span blue, 中等 %}

### 解题思路

~~硬生生把中等题写成了困难题~~

对 `words` 建立字典树，然后维护一个 `next: Map<char, Vec<Trie>>` 映射，表示从当前状态出发，接收一个字符 `char` 能够访问到的节点集合，然后对于输入序列，不断更新 next 集并统计答案：

```rust
use std::str::Chars;

macro_rules! ord {
    ($ch: expr) => {
        ($ch as usize - 'a' as usize)
    };
}

macro_rules! chr {
    ($id: expr) => {
        ((($id as u8) + b'a') as char)
    };
}

#[derive(PartialEq, Eq, Hash, Default)]
struct Trie {
    mark: i32,
    next: [Option<Box<Trie>>; 26],
}

impl Trie {  // 字典树
    fn insert(&mut self, mut chars: Chars) {
        if let Some(ch) = chars.next() {
            let index = ord!(ch);
            if matches!(self.next[index], None) {
                self.next[index] = Some(Box::new(Trie::default()))
            }
            self.next[index].as_mut().unwrap().insert(chars);
        } else {
            self.mark += 1;
        }
    }

    fn nexts(&self) -> Vec<(char, &Trie)> {  // 返回有效的 next
        self.next
            .iter()
            .enumerate()
            .filter_map(|(ch, node)| node.as_ref().map(|it| (chr!(ch), it.as_ref())))
            .collect()
    }
}

impl Solution {
    fn build(words: Vec<String>) -> Trie {  // 建树
        let mut root = Trie::default();
        for word in words {
            root.insert(word.chars().into_iter());
        }
        root
    }

    pub fn num_matching_subseq(seq: String, words: Vec<String>) -> i32 {
        let root = Self::build(words);

        let mut next: [Vec<_>; 26] = Default::default();
        let mut ans = 0;

        for (ch, node) in root.nexts() {
            next[ord!(ch)].push(node);
        }

        for ch in seq.chars() {
            for node in next[ord!(ch)].split_off(0) {
                ans += node.mark;  // 如果这是一个终态，则将其加到答案中
                for (ch, node) in node.nexts() {
                    next[ord!(ch)].push(node);
                }
            }
        }

        ans
    }
}
```

上面的代码偏工程性，且尚有可优化之处（例如 `Trie::nexts()` 可使用更高效的数据结构维护指向下一级的指针，需要时直接返回迭代器，避免遍历全部 26 个字母）

## 2022 年 11 月 16 日

* [775. 全局倒置与局部倒置](https://leetcode.cn/problems/global-and-local-inversions/)｜难度：{% span blue, 中等 %}

### 解题思路

乍一看像是求逆序对的题，但是题目只要求我们输出 `true` 或 `false`，并不需要求出具体数量，这就和 2022 年 10 月 10 日题目中「数组切分」的思想很相似了，只有数组中所有元素偏离原位置（排序后的位置）不超过 1，才可能满足题目条件：

```rust
impl Solution {
    pub fn is_ideal_permutation(nums: Vec<i32>) -> bool {
        for (i, x) in nums.into_iter().enumerate() {
            if (i as i32 - x).abs() > 1 {
                return false;
            }
        }
        true
    }
}

```

## 2022 年 11 月 15 日

* [1710. 卡车上的最大单元数](https://leetcode.cn/problems/maximum-units-on-a-truck/)｜难度：{% span green, 简单 %}

### 解题思路

贪心求解，尽可能选择单元数更多的箱子。

```rust
impl Solution {
    pub fn maximum_units(mut box_types: Vec<Vec<i32>>, mut truck_size: i32) -> i32 {
        box_types.sort_by_key(|it| -it[1]);

        let mut ans = 0;

        for it in box_types {
            if truck_size > it[0] {
                ans += it[0] * it[1];
                truck_size -= it[0];
            } else {
                ans += truck_size * it[1];
                break;
            }
        }

        ans
    }
}

```

## 2022 年 11 月 14 日

* [805. 数组的均值分割](https://leetcode.cn/problems/split-array-with-same-average/)｜难度：{% span red, 困难 %}

### 解题思路

dp 确实不咋会做（

看了题解说还可以折半搜索，重新捋一捋思路🤔。设总体和为 $S$，大小为 $N$，划分的两部分大小为 $N_1$、$N_2$，总和为 $S_1$、$S_2$，则有：

$$
\begin{align*}
\frac{S_1}{N_1} &= \frac{S_2}{N_2} \\
S_1 N_2 &= S_2 N_1 \\
S_1 N_2 + S_1 N_1 &= S_2 N_1 + S_1 N_1 \\
S_1 (N_1 + N_2) &= (S_1 + S_2) N_1 \\
S_1 N &= S N_1 \\
\frac{S_1}{N_1} &= \frac{S}{N}
\end{align*}
$$

也就是说，当数组的某一部分均值与整体均值相等的时候，一定能划分为满足条件的两组。但如果我们如此暴力枚举所有可能的组合，即使只考虑 $N_1 < \frac{N}{2}$ 的情况，也依然有 $2^{N-1} = 2^{29}$ 种情况，如此便会超时。

但是转念一想，这不就是 [两数之和](https://leetcode.cn/problems/two-sum/) 嘛！我们可以将数组平均划分为 $S_L$、$S_R$ 两部分，每一部分的大小为 $\frac{N}{2}$，暴力枚举 $S_R$ 所有子集的 $N_R'$ 和 $S_R'$，并将 $SN_R' - NS_R'$ 存入 Hash 表中（后面会讲到为何存这个数），然后枚举 $S_L$ 的子集，若存在：

$$
\frac{S_L' + S_R'}{N_L' + N_R'} = \frac{S}{N} \\ \quad \\
\begin{align*}
N S_L' + N S_R' &= S N_L' + S N_R' \\
N S_L' - S N_L' &= S N_R' - N S_R'
\end{align*}
$$

借助 Hash 表，我们便可以在 $O(1)$ 时间内检查 $N_L'$、$S_L'$ 是否满足条件。

```rust
use std::collections::HashMap;

impl Solution {
    pub fn split_array_same_average(nums: Vec<i32>) -> bool {
        let (n, s) = (nums.len(), nums.iter().sum::<i32>());
        let (left, right) = (&nums[..n / 2], &nums[n / 2..]);

        if n == 1 {  // 特判只有一个元素的情况
            return false;
        }

        let mut dict: HashMap<_, _> = HashMap::new();

        for x in 1..1 << right.len() {
            let (mut sp, mut np) = (0, 0);
            for i in 0..right.len() {
                if (1 << i) & x != 0 {
                    sp += right[i];
                    np += 1;
                }
            }
            let magic = s * np - n as i32 * sp;
            if magic == 0 {  // R 满足条件
                return true;
            }
            dict.insert(magic, np);
        }

        for x in 1..1 << left.len() {
            let (mut sp, mut np) = (0, 0);
            for i in 0..left.len() {
                if (1 << i) & x != 0 {
                    sp += left[i];
                    np += 1;
                }
            }
            let magic = n as i32 * sp - s * np;
            if magic == 0 {  // L 满足条件
                return true;
            }
            if let Some(nr) = dict.get(&magic) {  // 找到符合条件的 L', R' 且 L' + R' != nums
                if np + nr != n as i32 {
                    return true;
                }
            }
        }

        false
    }
}

```

此题各种边界情况比较多，需要注意特判，此外上面的代码比较混乱，我们可以整理一下代码使其更加优雅：

```rust
use std::collections::HashMap;

impl Solution {
    pub fn split_array_same_average(mut nums: Vec<i32>) -> bool {
        let (n, s) = (nums.len(), nums.iter().sum::<i32>());
        let right = nums.split_off(n / 2);

        if n == 1 {  // 特判只有一个元素的情况
            return false;
        }

        let mut dict: HashMap<_, _> = HashMap::new();
        let select = |arr: Vec<i32>| {
            (1 .. 1 << arr.len()).map(move |x| {
                let (mut sp, mut np) = (0, 0);
                for i in 0 .. arr.len() {
                    if (1 << i) & x != 0 {
                        sp += arr[i];
                        np += 1;
                    }
                }
                (s * np - n as i32 * sp, np)
            })
        };

        for (magic, np) in select(nums) {
            if magic == 0 {  // L 满足条件
                return true;
            }
            dict.insert(magic, np);
        }

        for (magic, np) in select(right) {
            if magic == 0 {  // R 满足条件
                return true;
            }
            match dict.get(&-magic) {  // 找到符合条件的 L', R' 且 L' + R' != nums
                Some(nr) if np + nr != n as i32 => return true,
                _ => ()
            }
        }

        false
    }
}
```

折半搜索，时间复杂度 $O((\sqrt{2})^N)$

## 2022 年 11 月 13 日

锵锵复活～

电脑还没修好，但我不能再坐以待毙了！于是把笔记本的 Windows 扬了，腾出 1T 的空闲来，把台式机的硬盘整个 dd 进去，几番折腾终于秽土转生……

* [791. 自定义字符串排序](https://leetcode.cn/problems/custom-sort-string/)｜难度：{% span blue, 中等 %}

### 解题思路

简单排序题，提前规划好 `index` 可以加速计算：

```rust
impl Solution {
    #[inline]
    fn ord(ch: char) -> usize {
        ch as usize - 'a' as usize
    }

    pub fn custom_sort_string(order: String, s: String) -> String {
        let mut chars: Vec<_> = s.chars().collect();

        let mut index = vec![0; 26];
        for (i, ch) in order.chars().enumerate() {
            index[Self::ord(ch)] = i;
        }

        chars.sort_by_key(|it| index[Self::ord(*it)]);
        chars.into_iter().collect()
    }
}
```

## 寄！

电脑寄了（悲

维修师傅让把 CPU 和主板寄回去返厂，结果到了让技术员测试又说没有任何问题，几番沟通之后现在又怀疑是显卡的问题，害……

## 2022 年 11 月 01 日

* [1662. 检查两个字符串数组是否相等](https://leetcode.cn/problems/check-if-two-string-arrays-are-equivalent/)｜难度：{% span green, 简单 %}

### 解题思路

这真的有什么好解释的么🤔

```rust
impl Solution {
    pub fn array_strings_are_equal(word1: Vec<String>, word2: Vec<String>) -> bool {
        word1.join("") == word2.join("")
    }
}
```

## 2022 年 10 月 31 日

* [481. 神奇字符串](https://leetcode.cn/problems/magical-string/)｜难度：{% span blue, 中等 %}

### 解题思路

模拟嘛，只要按照题目的意思构造一个序列出来就行了。用一个 `index` 记录当前规则（放几个），然后循环向数组里 push：

```rust
impl Solution {
    pub fn magical_string(n: i32) -> i32 {
        let mut arr = vec![1];
        let mut index = 1;

        while arr.len() < n as _ {
            let what = 3 - arr.last().unwrap();

            arr.push(what);  // 先放一个
            if arr[index] == 2 { arr.push(what); }  // 如果需要的话再放一个

            index += 1;
        }

        arr.into_iter().take(n as _).filter(|it| *it == 1).sum()
    }
}
```

除了打表之外貌似没有时间复杂度小于 $O(n)$ 的解法🤔

## 2022 年 10 月 30 日

* [784. 字母大小写全排列](https://leetcode.cn/problems/letter-case-permutation/)｜难度：{% span blue, 中等 %}

### 解题思路

其实关键并不在于如何 AC，而是如何优雅地 AC：

```rust
impl Solution {
    pub fn letter_case_permutation(s: String) -> Vec<String> {
        let chars: Vec<_> = s.to_lowercase().chars().collect();

        let mut mask = 1;
        let index: Vec<_> = chars.iter().map(|ch| {
            if ch.is_ascii_digit() {
                0
            } else {
                let backup = mask;
                mask <<= 1;
                backup
            }
        }).collect();

        let mut ans = vec![];
        for i in 0 .. mask {
            ans.push(
                chars.iter().zip(index.iter()).map(|(ch, mask)| {
                    if mask & i != 0 {
                        ((*ch as u8) - 32) as char
                    } else {
                        *ch
                    }
                }).collect()
            );
        }

        ans
    }
}
```

## 2022 年 10 月 29 日

* [1773. 统计匹配检索规则的物品数量](https://leetcode.cn/problems/count-items-matching-a-rule/)｜难度：{% span green, 简单 %}

### 解题思路

十分适合新手的一道题，练习 `match` 的使用（

```rust
impl Solution {
    pub fn count_matches(items: Vec<Vec<String>>, rule_key: String, rule_value: String) -> i32 {
        let mut ans = 0;

        for item in items {
            ans += match rule_key.as_str() {
                "type" => item[0] == rule_value,
                "color" => item[1] == rule_value,
                "name" => item[2] == rule_value,
                _ => panic!()
            } as i32;
        }

        ans
    }
}
```

## 2022 年 10 月 22 日 ～ 2022 年 10 月 28 日

* [Hackergame 2022](https://hack.lug.ustc.edu.cn/)｜难度：{% span purple, 噩梦 %}

一年一度的 Hackergame 开赛，我就不一心二用了，比赛十分精彩，欢迎各位前来体验！

## 2022 年 10 月 21 日

* [901. 股票价格跨度](https://leetcode.cn/problems/online-stock-span/)｜难度：{% span blue, 中等 %}

### 解题思路

记录每个位置向前最大跨度的下标，这样后续搜索时就能够跳过这些位置，从而实现加速：

```rust
struct StockSpanner {
    price: Vec<i32>,
    prev: Vec<usize>,
}

impl StockSpanner {
    fn new() -> Self {
        Self {
            price: vec![],
            prev: vec![],
        }
    }

    fn next(&mut self, price: i32) -> i32 {
        self.price.push(price);

        let length = self.prev.len();
        let mut index = length;
        while index >= 1 && self.price[length] >= self.price[index - 1] {
            index = self.prev[index - 1];
        }
        self.prev.push(index);

        (length - index + 1) as _
    }
}
```

复杂度似乎是 $O(n)$ 的，但是为什么这么慢🤔，可能是常数比官方题解的单调栈大（？

## 2022 年 10 月 20 日

* [779. 第K个语法符号](https://leetcode.cn/problems/k-th-symbol-in-grammar/)｜难度：{% span blue, 中等 %}

### 解题思路

* 解法一：递归

用数组 `F[i, j]` 表示第 `n - 1` 行，下标 `k - 1` 的元素，不难得到递推表达式为 `F[0, 0] = 0`、`F[i, j] = F[i - 1, j >> 1] ^ (j & 1)`，将其表示为递归形式即可。时间复杂度 $O(\log k)$，但是递归会产生一定开销

* 解法二：位运算

找规律（不会证😭），可知 `k - 1` 的二进制表示中 `1` 的数量就是答案：

```rust
impl Solution {
    pub fn kth_grammar(n: i32, mut k: i32) -> i32 {
        let mut ans = 0;
        k -= 1;
        while k != 0 {
            k ^= (k & -k);
            ans ^= 1;
        }
        ans
    }
}
```

最坏情况下，时间复杂度 $O(\log k)$，最好情况下，只需要 $O(1)$ 时间

## 2022 年 10 月 19 日

* [1700. 无法吃午餐的学生数量](https://leetcode.cn/problems/number-of-students-unable-to-eat-lunch/)｜难度：{% span green, 简单 %}

### 解题思路

统计出两种学生的数量，然后扫描三明治数组，当有三明治无法被消耗时退出循环，或完成遍历后返回 0（所有人都有得吃）

```rust
impl Solution {
    pub fn count_students(students: Vec<i32>, sandwiches: Vec<i32>) -> i32 {
        let mut count = [0; 2];
        count[0] = students.iter().filter(|it| **it == 0).count();
        count[1] = students.iter().filter(|it| **it == 1).count();

        for (i, it) in sandwiches.iter().enumerate() {
            let it = *it as usize;
            if count[it] > 0 {
                count[it] -= 1;
            } else {
                return (students.len() - i) as _;
            }
        }

        0
    }
}
```

昨天忘记更新博客了 qwq

## 2022 年 10 月 18 日

* [902. 最大为 N 的数字组合](https://leetcode.cn/problems/numbers-at-most-n-given-digit-set/)｜难度：{% span red, 困难 %}

### 解题思路

样例 2 已经在疯狂暗示，在一定范围内这个问题只是简单的等比求和，所以我们只需要特殊处理最后非等比的一小段即可。用数组 `dp[i][j]` 表示无 n 限制下，长度为 `i`，最高位小于等于 `j` 时解的数量，可以将问题分解为「比 `n` 位数少的」和「与 `n` 位数相同的」求解：

```rust
use std::collections::HashSet;

impl Solution {
    pub fn at_most_n_given_digit_set(digits: Vec<String>, mut n: i32) -> i32 {
        // 转换为 HashSet<i32>
        let digits: HashSet<_> = digits.iter().map(|it| it.as_bytes()[0] as usize - 0x30).collect();

        // n 拆分成 Vec<i32>
        let split = {
            let mut tmp = vec![];
            while n != 0 {
                tmp.insert(0, n as usize % 10);
                n /= 10;
            }
            tmp
        };
        let length = split.len();

        // 生成数组 dp
        let mut dp = [[0; 10]; 11];
        for i in 1 ..= length {
            for j in 1 ..= 9 {
                if i == 1 {
                    dp[i][j] = dp[i][j - 1] + if digits.contains(&j) { 1 } else { 0 };
                } else {
                    dp[i][j] = dp[i - 1][j] * digits.len();
                }
            }
        }

        let mut ans = 0;

        // 比 n 位数少的
        for row in &dp[1 .. length] {
            ans += row[9];
        }

        // 与 n 位数相同的
        for i in 0 .. length {
            let x = split[i];
            ans += dp[length - i][x.saturating_sub(1)];
            if i == length - 1 && digits.contains(&x) {
                ans += 1;
            }
            if !digits.contains(&x) {
                break;
            }
        }

        ans as _
    }
}

```

## 2022 年 10 月 17 日

* [904. 水果成篮](https://leetcode.cn/problems/fruit-into-baskets/)｜难度：{% span blue, 中等 %}

### 解题思路

滑动窗口的思想，用一个双向队列实现，循环中每轮先摘水果 push 到队尾，然后检查种类数是否满足要求，如果不满足就一直从队头 pop，直到满足要求为止，循环过程中记录一下滑动窗口的最大长度：

```rust
use std::cmp;
use std::collections::VecDeque;

struct Basket(Vec<(i32, usize)>);

impl Basket {
    fn new() -> Self {
        Self(vec![])
    }

    fn types(&self) -> usize {
        self.0.len()
    }

    fn add(&mut self, key: i32) {
        for pair in &mut self.0 {
            if pair.0 == key {
                pair.1 += 1;
                return;
            }
        }
        self.0.push((key, 0));
    }

    fn remove(&mut self, key: i32) {
        let mut index = usize::MAX;
        for (i, pair) in self.0.iter_mut().enumerate() {
            if pair.0 == key {
                if pair.1 > 0 {
                    pair.1 -= 1;
                    return;
                } else {
                    index = i;
                    break;
                }
            }
        }
        self.0.remove(index);
    }
}

impl Solution {
    pub fn total_fruit(fruits: Vec<i32>) -> i32 {
        let mut window = VecDeque::new();
        let mut basket = Basket::new();

        let mut ans = 0;
        for color in fruits {
            window.push_back(color);
            basket.add(color);

            while basket.types() > 2 {  // 种类数 > 2
                basket.remove(window.pop_front().unwrap());
            }

            ans = cmp::max(ans, window.len());
        }

        ans as _
    }
}
```

## 2022 年 10 月 16 日

* [886. 可能的二分法](https://leetcode.cn/problems/possible-bipartition/)｜难度：{% span blue, 中等 %}

### 解题思路

将所有人分为 3 个集合：`S`、`T` 和 `None`，初始所有人均位于 `None` 集中。考虑广度优先搜索，我们将一号节点加入待处理队列和 `S` 集，每次从待处理队列中取出一个节点，检查他与仇敌是否在同一个集合，是则直接返回 `false`，否则将仇敌加入对立集合和处理队列

注意考虑节点之间没有任何直接或间接联系时的处理方式：

```rust
use std::collections::{BTreeMap, VecDeque};

impl Solution {
    pub fn possible_bipartition(n: i32, dislikes: Vec<Vec<i32>>) -> bool {
        let mut group = vec![0; n as _];  // 1:S, -1:T, 0:None

        let dislikes = {  // 预处理 dislikes 为 map 类型
            let mut tmp: BTreeMap<usize, Vec<usize>> = BTreeMap::new();
            for pair in dislikes {
                let mut pair: Vec<_> = pair.iter().map(|it| *it as usize - 1).collect();
                for _ in 0 .. 2 {
                    if let Some(list) = tmp.get_mut(&pair[0]) {
                        list.push(pair[1]);
                    } else {
                        tmp.insert(pair[0], vec![pair[1]]);
                    }
                    pair.reverse();
                }
            }
            tmp
        };

        for i in 0 .. n as _ {
            if group[i] != 0 { continue; }  // 已经处理过的跳过

            let mut task = VecDeque::from([i]);
            group[i] = 1;  // 任意加入一组

            while let Some(now) = task.pop_front() {
                if let Some(opponents) = dislikes.get(&now) {
                    for op in opponents {
                        if group[*op] == group[now] { return false; }  // 发现仇人和自己在一组

                        if group[*op] == 0 {
                            group[*op] = -group[now];  // 把仇人放到另一组
                            task.push_back(*op);  // 仇人加入处理队列
                        }
                    }
                }
            }
        }

        true
    }
}
```

* 建图的时候直接 `BTreeMap` 摆烂了，用前向星存图可以更快

## 2022 年 10 月 15 日

* [1441. 用栈操作构建数组](https://leetcode.cn/problems/build-an-array-with-stack-operations/)｜难度：{% span blue, 中等 %}

### 解题思路

基本思想：

* 每轮先插入一个 `Push`，然后如果不需要这个数，就再插入一个 `Pop`
  
* 如果已经达到要求，则退出循环

```rust
impl Solution {
    pub fn build_array(target: Vec<i32>, n: i32) -> Vec<String> {
        let mut size = 0;
        let mut output = Vec::new();

        for i in 1 ..= n {
            output.push(String::from("Push"));
            
            if target[size] != i {
                output.push(String::from("Pop"));
            } else {
                size += 1;
            }
            
            if size == target.len() {
                break;
            }
        }

        output
    }
}
```

## 2022 年 10 月 14 日

* [940. 不同的子序列 II](https://leetcode.cn/problems/distinct-subsequences-ii/)｜难度：{% span red, 困难 %}

### 解题思路

#### 朴素算法

看到取模 `1e9 + 7` 直接一眼定真：动态规划，然后来想想状态如何建立🤔。不妨用状态数组 $dp_{ch,j}$ 表示以字符 $ch$ 结尾、长度为 $j + 1$ 的字序列数量，那么有状态转移方程：

$$
dp_{ch, j} = \begin{cases}
1 & j = 0 \\
\sum dp_{*, j - 1} & j > 0
\end{cases}
$$

当长度为 1 时，字序列就是字符 $ch$ 本身；否则可从长度为 $j$ 的字序列通过末尾添加字符 $ch$ 得到，所以是上一列的求和。转移方程十分简单，但是更新数组 $dp$ 的顺序很重要，为了避免新添加的字符被重复计算，需要从后往前依次更新 $dp$。例如对于字符串 `abca`，有：

```text
# 初始化所有元素为 0（未考虑到的部分用「-」标记）
 dp | 0 1 2 3
----+---------
'a' | - - - -
'b' | - - - -
'c' | - - - -

1. 处理字符 'a' 后
 dp | 0 1 2 3
----+---------
'a' | 1 - - -
'b' | 0 - - -
'c' | 0 - - -

2. 处理字符 'c' 后
 dp | 0 1 2 3
----+---------
'a' | 1 0 - - 
'b' | 0 0 - -
'c' | 1 1 - -

3. 处理字符 'b' 后
 dp | 0 1 2 3
----+---------
'a' | 1 0 0 -
'b' | 1 2 1 -
'c' | 1 1 0 -

4. 处理字符 'c' 后
 dp | 0 1 2 3
----+---------
'a' | 1 0 0 0
'b' | 1 2 1 0
'c' | 1 3 3 1
```

最后把数组元素全部加起来（注意取模），就是最终的答案，下面是 rust 代码实现：

```rust
impl Solution {
    pub fn distinct_subseq_ii(s: String) -> i32 {
        const MOD: usize = 1_000_000_007;
        const LETTERS: usize = 26;

        let n = s.len();
        let s: Vec<_> = s.chars().collect();

        let mut ans = 0;
        let mut dp = vec![vec![0; n]; LETTERS];

        for i in 0 .. n {
            let ch = s[i] as usize - 'a' as usize;
            for j in (0 ..= i).rev() {
                dp[ch][j] = if j == 0 {
                    1
                } else {
                    let mut sum = 0;
                    for k in 0 .. LETTERS {
                        sum = (sum + dp[k][j - 1]) % MOD;
                    }
                    sum
                }
            }
        }

        for i in 0 .. n {
            for j in 0 .. LETTERS {
                ans = (ans + dp[j][i]) % MOD;
            }
        }

        ans as i32
    }
}
```

朴素算法的时间复杂度为 $O(n^2m)$，$m$ 为字符集大小，会超时。

#### 性能调优

再一看，似乎没有必要每次都重新计算每列的总和，考虑引入一个数组 `sum`，动态地维护每次变化的量，可以将时间复杂度优化到 $O(n^2)$：

```rust
impl Solution {
    pub fn distinct_subseq_ii(s: String) -> i32 {
        const MOD: usize = 1_000_000_007;

        let n = s.len();
        let s: Vec<_> = s.chars().collect();

        let mut ans = 0;
        let mut dp = vec![vec![0; n]; 26];
        let mut sum = vec![0; n];

        for i in 0 .. n {
            let ch = s[i] as usize - 'a' as usize;
            for j in (0 ..= i).rev() {
                let new = if j == 0 {
                    1
                } else {
                    sum[j - 1]
                };
                sum[j] = (sum[j] + MOD + new - dp[ch][j]) % MOD;
                dp[ch][j] = new;
            }
        }

        for i in 0 .. n {
            ans = (ans + sum[i]) % MOD;
        }

        ans as i32
    }
}
```

能 AC 了，但总感觉还是不够优雅。

#### 极致优化

这一次尝试再将数组 $dp$ 横向压缩，即 $dp_{ch}$ 表示当前已经考虑的部分，以字符 $ch$ 结尾的子序列数量，每当处理一个字符 $ch$，我们就把 $dp_{ch}$ 更新为 $\sum dp + 1$。还是以字符串 `acbc` 举例：

```text
# 初始化为全 0
dp = [0, 0, 0]

1. 处理字符 'a' 后
dp = [1, 0, 0]

2. 处理字符 'c' 后
dp = [1, 0, 2]

3. 处理字符 'b' 后
dp = [1, 4, 2]

4. 处理字符 'c' 后
dp = [1, 4, 8]
```

在遇到第二个字符 `c` 时，$dp$ 中的三个元素分布代表 `*a`、`*b`、`*c` 的数量，将字符 `c` 加在各字序列末尾，得到 `*ac`、`*bc`、`*cc`，又由于它们 `*` 部分各不相同，所以不会产生重复，最后再加上一个字符 `c` 本身，就是新的 $dp_c$ 的值。据此编写代码：

```rust
impl Solution {
    pub fn distinct_subseq_ii(s: String) -> i32 {
        const MOD: usize = 1_000_000_007;

        let mut dp = vec![0; 26];
        let mut sum = 0;

        for ch in s.chars() {
            let ch = ch as usize - 'a' as usize;
            let old = dp[ch];
            dp[ch] = sum + 1;
            sum = (sum + MOD - old + dp[ch]) % MOD;
        }

        sum as i32
    }
}
```

最终时间复杂度 $O(n)$，空间复杂度 $O(m)$

## 2022 年 10 月 13 日

* [769. 最多能完成排序的块](https://leetcode.cn/problems/max-chunks-to-make-sorted/)｜难度：{% span blue, 中等 %}

### 解题思路

#### 朴素算法

对于 `arr[i] = k`，若要满足题目要求，则至少区间 `[min(i, k), max(i, k)]` 会落在同一个分区中。那么只需遍历 `arr`，对每一个区间做并查集，统计最终的集合数量即可：

```rust
use std::cmp::{max, min};

impl Solution {
    pub fn max_chunks_to_sorted(arr: Vec<i32>) -> i32 {
        let n = arr.len();
        let mut dsu: Vec<_> = (0 .. n).collect();

        for i in 0 .. n {
            let (l, r) = (min(i, arr[i] as usize), max(i, arr[i] as usize));
            for j in l .. r {
                dsu[j] = r;
            }
        }

        let mut ans = 0;
        for i in 0 .. n {
            if dsu[i] == i { ans += 1; }
        }

        ans
    }
}
```

#### 性能调优

写完之后打眼一看，似乎并没有用到并查集「查」的功能；又由于 `arr` 中的元素有且仅有 `[1, n)` ，一个萝卜一个坑，错位的元素必然会组成循环，所以我们只需要统计 `k > i` 的情况。那么可以将代码优化成下面这样：

```rust
use std::cmp::max;

impl Solution {
    pub fn max_chunks_to_sorted(arr: Vec<i32>) -> i32 {
        let (n, mut ans) = (arr.len(), 0);
        let mut sign = 0;

        for i in 0 .. n {
            sign = max(sign, arr[i] as usize);  // 标记 [i, sign) 的元素皆为非根
            if sign == i { ans += 1; }  // 并查集之后作为根节点
        }

        ans
    }
}
```

最终时间复杂度 $O(n)$，空间复杂度 $O(1)$（以及不是很理解为什么题目数据范围是 `n <= 10`

## 2022 年 10 月 12 日

* [817. 链表组件](http://localhost:4000/posts/935157128/)｜难度：{% span blue, 中等 %}

* 不知道为什么会是中等题，就算不依赖标准库也完全可以排序 + 二分，算不上十分麻烦

### 解题思路

* 将 `nums` 处理成 `BTreeSet<i32>` 类型，方便快速查找

* 遍历链表，找出属于 `nums` 的连续的段即可

```rust
use std::collections::BTreeSet;

impl Solution {
    pub fn num_components(head: Option<Box<ListNode>>, nums: Vec<i32>) -> i32 {
        // 参数预处理
        let mut head = &head;
        let nums: BTreeSet<_> = nums.iter().collect();

        let mut ans = 0;
        let mut last = false;  // 记录上一个节点值是否属于 nums

        while let Some(node) = head {
            let now = nums.contains(&node.val);
            if now && !last {
                ans += 1;
            }
            last = now;
            head = &node.next;
        }

        if last { ans += 1; }  // 处理边界

        ans
    }
}
```

时间复杂度 $O(n \log n)$，空间复杂度 $O(n)$

## 2022 年 10 月 11 日

* [1790. 仅执行一次字符串交换能否使两个字符串相等](https://leetcode.cn/problems/check-if-one-string-swap-can-make-strings-equal/)｜难度：{% span green, 简单 %}

### 解题思路

~~三个 if，让 OJ 为我通过 18 个测试点：~~

* 若两字符串相等，直接返回 `true`

* 遍历寻找不同之处，记录到数组 `diff` 中，`diff` 的长度应恰好为 2

* 交换之后应相等

```rust
impl Solution {
    pub fn are_almost_equal(s1: String, s2: String) -> bool {
        if s1 == s2 { return true; }  // 若相等直接返回

        let a1: Vec<_> = s1.chars().collect();
        let a2: Vec<_> = s2.chars().collect();

        let mut diff = Vec::new();
        for i in 0 .. a1.len() {
            if a1[i] != a2[i] { diff.push(i); }
        }

        if diff.len() != 2 { return false; }  // 有且仅有两处不同

        a1[diff[0]] == a2[diff[1]] && a2[diff[0]] == a1[diff[1]]  // 交叉相等
    }
}
```

时间复杂度 $O(n)$，空间复杂度 $O(n)$

## 2022 年 10 月 10 日

* [801. 使序列递增的最小交换次数](https://leetcode.cn/problems/minimum-swaps-to-make-sequences-increasing/)｜难度：{% span red, 困难 %}

### 解题思路

拿到题目先贪它一把，从数组开头往后捋，一旦遇到违反递增规则的数就交换，记录交换的次数。同时不难注意到，交换 $k$ 次和交换 $N - k$ 次是一样的（$N$ 为数组长度），那么只需要在最后返回最小的那个……

```rust
use std::cmp::min;
use std::mem::swap;

impl Solution {
    pub fn min_swap(mut nums1: Vec<i32>, mut nums2: Vec<i32>) -> i32 {
        let n = nums1.len();
        let mut ans: usize = 0;

        for i in 1 .. n {
            if nums1[i - 1] >= nums1[i] || nums2[i - 1] >= nums2[i] {
                swap(&mut nums1[i], &mut nums2[i]);
                ans += 1;
            }
        }

        min(ans, n - ans) as i32
    }
}
```

然后 …… 意料之中的 WA 了，来看看导致错误的这组输入：

```text
nums1 = [0 4 4 5 9]
nums2 = [0 1 6 8 10]
```

按照我们的逻辑，将在 index 为 2 和 3 的时候对数组进行翻转，此时 `ans` 等于 2，返回的 `min(ans, n - ans)` 依然为 2 …… 问题出现了，翻转所有其它元素并不比翻转 `(4, 6)`、`(5, 8)` 两组的「开销」更低

注意到，在上述情况中，「翻转所有其它元素」其实并没有必要包含 `(0, 0)` 和 `(9, 10)` 这两对，因为它们无论如何翻转，都不会影响最终「严格递增」这一要求。所以不妨考虑首先将 `nums1` 和 `nums2` 进行分段，如果 `max(nums1[i - 1], nums2[i - 1]) < min(nums1[i], nums2[i])`，则进行一次切分。处理后的两个数组:

```text
nums1 = [0 | 4 4 5 | 9]
nums2 = [0 | 1 6 8 | 10]
```

切分出来的三段相互独立、互不影响，只需要对每一段都跑一次上面的贪心方法，然后将最终结果累加起来即可：

```rust
use std::cmp::{max, min};
use std::mem::swap;

impl Solution {
    pub fn min_swap(mut nums1: Vec<i32>, mut nums2: Vec<i32>) -> i32 {
        // 在数组末尾制造一次切分，简化后续代码
        nums1.push(i32::MAX); nums2.push(i32::MAX);
        let n = nums1.len();

        let mut ans: usize = 0;
        let mut index = 0;  // 区间左端点

        for i in 1 .. n {
            if max(nums1[i - 1], nums2[i - 1]) < min(nums1[i], nums2[i]) {
                let mut result = 0;  // 当前区间的开销
                for j in index .. i - 1 {  // 对区间做贪心求解
                    if nums1[j] >= nums1[j + 1] || nums2[j] >= nums2[j + 1] {
                        swap(&mut nums1[j + 1], &mut nums2[j + 1]);
                        result += 1;
                    }
                }
                ans += min(result, i - index - result);  // 结果累加到总开销
                index = i;
            }
        }

        ans as i32
    }
}
```

最终只对 `nums1` 和 `nums2` 做了两次遍历，时间复杂度 $O(n)$，空间复杂度 $O(1)$

## 2022 年 10 月 09 日

* [856. 括号的分数](https://leetcode.cn/problems/score-of-parentheses/)｜难度：{% span blue, 中等 %}

### 解题思路

* 维护一个栈，初始元素为 0

* 当遇到 `(` 时，将 `0` 压栈

* 遇到 `)` 时，将栈顶元素 `top` 弹出，如果为 0，则把此时的栈顶加 1；否则，加上 `top * 2`

```rust
impl Solution {
    pub fn score_of_parentheses(s: String) -> i32 {
        let mut stack = vec![0];

        for ch in s.chars() {
            match ch {
                '(' => stack.push(0),
                ')' => {
                    let top = stack.pop().unwrap();
                    let newtop = if top == 0 {
                        stack.pop().unwrap() + 1
                    } else {
                        stack.pop().unwrap() + top * 2
                    };
                    stack.push(newtop);
                }
                _ => panic!()
            }
        }

        stack[0]
    }
}
```

解释：`top` 为 0 时，意味着遇到了 `()`，计算结果为 1；不为 0 时，代表括号内包含其它内容，那么将其计算结果乘二后加到父级括号上。最终算法时间复杂度 $O(n)$，空间复杂度 $O(n)$：


