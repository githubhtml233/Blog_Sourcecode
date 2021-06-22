# 排序算法

时间复杂度：快些以nlog2n的速度归队
注解：平均情况下，快排、希尔、归并、堆排序时间复杂度均为$O(nlog_2n)$,其他均为$O(n^2)$,除了基数排序为O(d(n+rd))

空间复杂度：快排：$O(log_2n)$、归并排序O(n),基数排序O(rd),其他都是O(1)

稳定性：心情不稳定，快些选一堆朋友来聊天吧
**注解：**
快排、希尔、简单选择、堆排序。排序的稳定性指的是原始数组中有多个相同的关键字，经过排序后，其相对次序不发生变化，则称该排序算法为稳定的。


## 快速排序
**原理：**
通过选择基准，通过双指针分别从数组左右两侧向中间遍历，当右指针寻到比基准小的关键字，将该关键字移至左指针位置，然后切换左指针遍历，寻到比基准大的关键字时，将其移至右指针位置，当左右指针重合时，将基准移至该重合位置，此时基准左侧的关键字都比它小，右侧关键字都比它大，即此时基准落在它的最终排序位置，然后对以基准为分界的两个子数组重复进行上述操作，最终得到排序数组。代码实现如下。
```js
const quickSort = (arr, l, r) => {
    if (l < r) {
        if (arr.length <= 1) {
            return arr;
        }
        const x = arr[l]; //基准值
        let i = l, j = r;
        while (i < j) {
            //从右侧寻找第一个小于基准的值
            while (i < j && arr[j] >= x) {
                j--;
            }
            //找到值，将其移至左侧空处，i++减少重复对比
            if (i < j) {
                arr[i++] = arr[j];
            }
            //从左侧寻找第一个大于基准的值
            while (i < j && arr[i] <= x) {
               i++; 
            }
            //找到值，将其移至右侧空处，j--减少重复对比
            if (i < j) {
                arr[j--] = arr[i];
            }
        }
        //一次遍历结束，将x填至空处，此时x大于其左侧的值，小于右侧的值
        arr[i] = x;
        quickSort(arr, l, i - 1);
        quickSort(arr, i + 1, r);
    }
}
```
## 冒泡排序
**原理：**
比较相邻的元素，如果顺序错误，则交换元素。
```js
const bubbleSort = (arr, r) => {
    if (r === 0) {
        return;
    }
    for (let i = 0; i < r; i++) {
        if (arr[i] > arr[i + 1]) {
            [arr[i], arr[i + 1]] = [arr[i + 1], arr[i]];
        }
    }
    bubbleSort(arr, r - 1);
}
```
## 选择排序
**原理：**
每一次排序都对数组未排序部分进行遍历，选择最小的（大）的元素，放在已排序序列的末尾
## 插入排序
将第一个元素看作已排序序列，剩余元素看作未排序序列，从头到尾遍历数组，将扫描到的元素插入有序序列适当的位置，如果与已排序元素与待插入元素相同，则将待插入元素插入相同已排序元素后面
## 归并排序
**原理：**
以二路归并为例，将数组分为两个子数组，并将子数组不断二分得到仅为1个元素的子数组，然后将排好序的子数组不断合并成为一个大的顺序数组。
```js
//从上至下递归版
const mergeSort = arr => {
    const len = arr.length;
    if (len < 2) {
        return arr;
    }
    var middle = Math.floor(len / 2), 
        left = arr.slice(0, middle),
        right = arr.slice(middle);
    return merge(mergeSort(left), mergeSort(right));
}
//从下至上迭代版
const mergeSort = arr => {
    const len = arr.length;
    if (len < 2) {
        return arr;
    }
    const work = []; //避免奇数个元素情况下不能两两合并
    for (const val of arr) {
        work.push([val]);
    }
    work.push([]);
    for (let lim = len; lim > 1; lim = ~~((lim + 1) / 2)) { //每一次迭代代表一次完整的二路归并,~~相当于parseInt，>>1相当于除2并parseInt,不会四舍五入
        for (var j = 0, k = 0; k < lim; j++, k += 2) {
            work[j] = merge(work[k], work[k + 1]);
        }
        work[j] = []; //一轮合并完成，res最后项已合并，值存在work[j - 1]，因此置[]
    }
    return work[0];
}

const merge = (left, right) => {
    const res = [];
    while (left.length && right.length) {
        if (left[0] <= right[0]) {
            res.push(left.shift())
        }
        else {
            res.push(right.shift());
        }
    }
    while (left.length) {
        res.push(left.shift());
    }
    while (right.length) {
        res.push(right.shift());
    }
    return res;
}

```
## 堆排序
## 希尔排序
也叫作递减增量排序，首先将待排序数组分为多个子数组，分别进行插入排序，再对整体数组进行插入排序
## 桶排序
## 基数排序