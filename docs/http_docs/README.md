---
sidebar: auto
---

## 前端常见存储方式
cookie、localStorage和sessionStorage是三种前端本地存储方式，其中localStorage和sessionStorage是HTML5新增方式。localStorage 适合持久化缓存数据，比如页面的默认偏好配置等；sessionStorage 适合一次性临时数据保存。
**区别：**
cookie： 
- 在设置的过期日期前皆有效，若没设置则在关闭浏览器后失效
- 存储数据较小，4kb左右
- 在http请求中，始终被携带于HTTP头中，即使不需要
- 可在所有同源窗口共享

localStorage：
- 除非被手动清除，否则一直存在
- 可以保存5MB的信息（与sessionStorage一致）
- 仅在客户端保存（与sessionStorage一致）
- 可在所有同源窗口共享
  
sessionStorage：
- 仅在当前网页会话下有效，关闭页面或者浏览器后会被清楚
- 不在不同的浏览器窗口共享
  
## cookie和session
因为http是一个不保存状态的协议，也就是服务器并不知道是不是同一个浏览器在访问
Session、Cookie记录服务器和客户端会话状态的机制，用来跟踪浏览用户身份的会话方式；
**区别：**
- 安全性：Session比Cookie安全，Session存储在服务端，Cookie存储在客户端
- 存取值的类型不同：Cookie只支持字符串，Session无限制
- 有效期不同：Cookie可设置过期日期，而Session在客户端关闭和Session超时都会失效。
- 存储大小：Session远大于Cookie