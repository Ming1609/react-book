# 初学陷阱

## class&className

当你看到报错信息 `Warning: Unknown DOM property class. Did you mean className?` 时，说明你在 jsx 中使用了 `class="demo"`，应该使用 className

> 由于 JSX 就是 JavaScript，一些标识符像 class 和 for 不建议作为 XML 属性名。作为替代，React DOM 使用 className 和 htmlFor 来做对应的属性。

## <input>&<input/>

当你看到报错信息 `Expected corresponding JSX closing tag for input` 时，说明你标签没有闭合。

```html
x <input type="text">
✓ <input type="text" />
x <img src="" >
✓ <img src="" />
x <br>
✓ <br />
```

## key

当你看到报错信息 `Each child in an array or iterator should have a unique "key" prop` 时，说明你没有给循环输出的组件添加 `key` (`key` 可确保在组件更新时)

> 如果子组件位置会改变（如在搜索结果中）或者有新组件添加到列表开头（如在流中）情况会变得更加复杂。如果子级要在多个渲染阶段保持自己的特征和状态，在这种情况下，你可以通过给子级设置惟一标识的 key 来区分。

> 务必把key 添加到子级数组里组件本身上，而不是每个子级内部最外层 HTML 上

```js
var ListItemWrapper = React.createClass({
  render: function() {
    // 不要再 li 上加 key
    return <li>{this.props.data.text}</li>;
  }
});
var MyComponent = React.createClass({
  render: function() {
    return (
      <ul>
        {this.props.results.map(function(result, i) {
           // 应该在组件上加 key
           return <ListItemWrapper key={i} data={result}/>;
        })}
      </ul>
    );
  }
});
```

## jsx-wrap

> jsx 必须由一个标签包裹，顶级标签只允许有一个

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
// 正确
return (
    <span>
        <span>1</span>
        <span>2</span>
    </span>
)
```

## 受限组件

必须理解什么是受限组件，和表单在 React 中调用方式

Forms: http://reactjs.cn/react/docs/forms.html

## 中文输入法

使用 `onCompositionEnd` `onCompositionStart` `onCompositionUpdate` 解决中文输入法导致的 value 更新问题

## setState的延迟

> setState() 不会立刻改变 this.state，而是创建一个即将处理的 state 转变。在调用该方法之后获取 this.state 的值可能会得到现有的值，而不是最新设置的值。
> 不保证 setState() 调用的同步性，为了提升性能，可能会批量执行 state 转变和 DOM 渲染。

```js
// 通过 setTimeout 可让代码在 setState 应用到 DOM 中后执行
this.setState({
    value: 'abc'
})
setTimeout(function(){
    // some code
}, 0)
```
