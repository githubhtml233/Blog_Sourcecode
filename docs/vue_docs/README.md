---
sidebar: auto
---

## v-if vs v-show
"v-if"是真正的条件渲染，能确保在切换过程中中条件块内的事件监听器和子组件适当地被销毁和重建，且是惰性的，即若在初始渲染时条件为假，则什么也不做，直到条件第一次为真，才开始渲染条件块。
"v-show"不管初始条件是什么都会进行渲染，只是基于CSS"dispaly:none"进行切换。
## v-for 与 key
**为什么v-for要与key一起使用：**
为了给Vue一个提示，使其能跟踪每个节点的身份。从而重用和重新排序现有元素
## v-if 与 key
管理可复用元素，保证元素独立，不要就地复用。
## v-for 不推荐与 v-if 一起使用
当他们处于同一节点，"v-for"的优先级比"v-if"高，意味着"v-if"将分别重复运行于每个"v-for"循环中。仅适合与想为部分项渲染节点的情况。
##调试经验
    bug信息：使用vue init webpack my-project报错：vue-cli · Failed to download repo vuejs-templates/webpack: connect ETIMEDOUT 192.30.253.113:443
    推测原因：github无法链接。
    解决办法：下载本地webpack并使用vue init webpack my-project --offline
