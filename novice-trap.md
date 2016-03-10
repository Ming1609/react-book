# 初学陷阱

> 先列出简单目录，后续更新详细说明

`class="demo"` x  `className="demo"` ✓

---

`<input type="text" >` x  `<input type="text" />` ✓

---

`<Item />` x  `<Item key={"key" + i} />` ✓

```js
{
                // forEach 不适用当前场景
    ['a','b','c'].map(function(item, i){
        // <Item text={item} /> x
        return (
          <Item text={item} key={"key" + i} />
        )
    })
}
```
---

```js
// 错误
return (
    <span>1</span>
    <span>2</span>
)
// 正确
return (
    <div>
        <span>1</span>
        <span>2</span>
    </div>
)
```

---

**Forms:* http://reactjs.cn/react/docs/forms.html

---

如何修改受限的 `<input type="checkbox"  />

---

`<input onChange={this.saveValue} value={this.state.value} />` 碰上中文输入法会出现 `wenzi文字` ,需要用 `defaultValue` 替代 `value`

---

`<textarea>abc</textarea>` x  `<textarea value="abc" />` ✓

---
