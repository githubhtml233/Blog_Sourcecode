# 回溯算法
- 回溯算法是一种暴力穷举算法
- 穷举的过程是一个遍历多叉树的过程
- 回溯算法的遍历框架和多叉树的遍历框架类似
- 一般是应用于求所有的可行解
- 可认为是dfs算法
- 时间复杂度较高。计算方法为递归函数本身的复杂度乘递归函数被调用的次数
```js
//回溯算法框架
const backTrack = (path, selectList) => {
    if (满足结束条件) {
        res.push(路径);
        return;
    }
    for (const selcet of selectList) {
        做选择;
        backTrack(path, selectList);
        撤销选择;
    }
}
//多叉树遍历框架
cosnt traverse = (treeNode, root) => {
    if (root === null) {
        return;
    }
    for (const childNode of root.children) {
        traverse(childNode);
    }
}
```
##经典回溯问题
###全排列
给定一个不含重复数字的数组 nums ，返回其所有可能的全排列你可以按任意顺序返回答案。
```js
var permute = function(nums) {
    //记录路径
    const track = [],
          res = [];
    const backTrack = (nums, track) => {
        //到达叶子节点，将路径装入结果列表
        if (track.length === nums.length) {
            res.push(track.slice());
            return;
        }
        for (const val of nums) {
            //排除不合法的选择
            if (track.indexOf(val) !== -1) {
                continue;
            }
            //做选择
            track.push(val);
            //进入下一层决策树
            backTrack(nums, track);
            //取消选择
            track.pop();
        }
    }
    backTrack(nums, track);
    return res;
}
```