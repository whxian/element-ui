#### 去除table排序上下箭头中间空挡

源码中增加以下代码

---

```javascript
return !order ? 'ascending' : order === 'ascending' ? 'descending' : 'ascending';
```
