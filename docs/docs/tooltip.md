## Tooltip 文字提示

常用于展示提示信息。

### 引入

```json
{
  "usingComponents": {
    "wd-tooltip": "/wot-design/tooltip/index"
  }
}
```

### 基本用法

在这里我们提供 12 种不同方向的展示方式，可以通过以下完整示例来理解，选择你要的效果。

使用`content`属性来决定显示时的提示信息。
由`placement`属性决定展示效果：`placement`属性值为：`方向-对齐位置`；四个方向：`top`、`left`、`right`、`bottom`；三种对齐位置：`start`, `end`，默认为空。如`placement="left-end"`，则提示信息出现在目标元素的左侧，且提示信息的底部与目标元素的底部对齐。

```html
<view>
  <view class="top">
    <wd-tooltip placement="top" content="top 提示文字">
      <wd-button>top</wd-button>
    </wd-tooltip>
  </view>
  <view class="top">
    <wd-tooltip placement="top-start" content="top-start 提示文字">
      <wd-button>top-start</wd-button>
    </wd-tooltip>
  </view>
</demo-block>
  <view class="top">
    <wd-tooltip placement="top-end" content="top-end 提示文字">
      <wd-button >top-end</wd-button>
    </wd-tooltip>
  </view>
  <view class="bottom">
    <wd-tooltip placement="bottom" content="bottom 提示文字">
      <wd-button >bottom</wd-button>
    </wd-tooltip>
  </view>
  <view class="bottom">
    <wd-tooltip placement="bottom-start" content="bottom-start 提示文字">
      <wd-button >bottom-start</wd-button>
    </wd-tooltip>
  </view>
  <view class="bottom">
    <wd-tooltip placement="bottom-end" content="bottom-end 提示文字">
      <wd-button >bottom-end</wd-button>
    </wd-tooltip>
  </view>
</demo-block>
  <view class="left">
    <wd-tooltip placement="left" content="left 提示文字">
      <wd-button >left</wd-button>
    </wd-tooltip>
  </view>
  <view class="left">
    <wd-tooltip placement="left-start" content="left-start 提示文字">
      <wd-button >left-start</wd-button>
    </wd-tooltip>
  </view>
  <view class="left">
    <wd-tooltip placement="left-end" content="left-end 提示文字">
      <wd-button >left-end</wd-button>
    </wd-tooltip>
  </view>
  <view class="right">
    <wd-tooltip placement="right" content="right 提示文字">
      <wd-button >right</wd-button>
    </wd-tooltip>
  </view>
  <view class="right">
    <wd-tooltip placement="right-start" content="right-start 提示文字">
      <wd-button >right-start</wd-button>
    </wd-tooltip>
  </view>
  <view class="right">
    <wd-tooltip placement="right-end" content="right-end 提示文字">
      <wd-button >right-end</wd-button>
    </wd-tooltip>
  </view>
</view>
```

```css
.top{
  margin: 40px auto 0;
  width: 80%;
  text-align: center;
}
.bottom {
  width: 80%;
  text-align: center;
  margin: 0 auto 90px;
}
.left,
.right{
  width: 80%;
  text-align: center;
  margin: 40px;
}
```

### 主题

Tooltip 组件提供了两个不同的主题：`dark`和`light`。

通过设置`effect`属性来改变主题，默认为`dark`。

```html
<wd-tooltip content="dark 默认风格">
  <wd-button >dark</wd-button>
</wd-tooltip>
<wd-tooltip effect="light" content="light 风格">
  <wd-button >light</wd-button>
</wd-tooltip>
```

### 更多 Content

展示多行文本或者是设置文本内容的格式

用具名 slot 分发`content`，替代 `tooltip` 中的 `content` 属性。
使用插槽时，请使用 `useContentSlot` 属性，确定 `content` 插槽开启。

```html
<wd-tooltip placement="right" useContentSlot>
  <wd-button >多行文本</wd-button>
  <view slot="content" style="color: red; padding: 5px; width: 90px">
    <view>多行文本1</view>
    <view>多行文本2</view>
    <view>多行文本3</view>
  </view>
</wd-tooltip>
```

### 模式 mode

使用 `mode` 属性控制当前文字提示的模式。

`mode` 有两个值，一种是 `normal` 普通文字模式，另一种是 `menu` 列表模式。

`mode` 默认值为 `normal`，当 `mode` 处于默认状态，`content` 属性传入要显示的 `String` 字符串。

当 `mode` 为 `menu` ，文字提示框会展示成列表形式，此时 `content` 属性传入 `Array` 类型，数组中每一个对象以 `[{ name: 'person', content: '内容' }]` 命名。如果不需要icon，那么传入 `[{ content: '内容' }]`。

```html
<wd-tooltip placement="bottom" mode="menu" content="{{ menu }}" bind:menu-click="link">
  <wd-button >列表</wd-button>
</wd-tooltip>
```

```javascript
Page({
  data: {
    menu: [
      {
        name: 'person',
        content: '全部标记已读'
      },
      {
        name: 'close-fill',
        content: '清空最近会话'
      }
    ]
  },
  link (item) {
    console.log('调用', item)
  }
})
```

### 高级扩展

除了这些基本设置外，还有一些属性可以让使用者更好的定制自己的效果：

如果需要关闭 `tooltip` 功能，`disabled` 属性可以满足这个需求，它接受一个`Boolean`，设置为`true`即可。

```html
<wd-tooltip placement="right-end" content="禁用" disabled>
  <wd-button >禁用</wd-button>
</wd-tooltip>
```

### 控制位置

**注意：由于微信小程序无法动态插入节点，因此文字气泡位置会根据传入定位的节点最外层位置对齐，如果文字提示位置不在您想要渲染的位置上，可以通过控制组件整体位置达到想要的效果。**
错误用法示例：

```html
<wd-tooltip placement="top" content="top 提示文字" >
  <wd-button style="margin-left: 100px">top</wd-button>
</wd-tooltip>
<wd-tooltip placement="top" content="top 提示文字" >
  <wd-button style="position: absolute; left: 100px;">top</wd-button>
</wd-tooltip>
```

正确用法：

```html
<wd-tooltip placement="top" content="top 提示文字" style="margin-left: 100px">
  <wd-button>top</wd-button>
</wd-tooltip>
<wd-tooltip placement="top" content="top 提示文字" style="position: absolute; left: 100px;">
  <wd-button>top</wd-button>
</wd-tooltip>
```

### Tooltip Attributes

| 参数               | 说明                                                     | 类型              | 可选值      | 默认值 |
|--------------------|----------------------------------------------------------|-------------------|-------------|--------|
|  effect        |  默认提供的主题  | String            | dark/light | dark  |
|  show |  状态是否可见  | Boolean           | — |  false |
|  content        |  显示的内容，也可以通过 `slot#content` 传入  | String/Array            | — | — |
|  placement        |  Tooltip 的出现位置  | String           |  top/top-start/top-end/bottom/bottom-start/bottom-end/left/left-start/left-end/right/right-start/right-end |  bottom |
|  disabled       |  Tooltip 是否可用  | Boolean           | — |  false |
|  visible-arrow   |  是否显示 Tooltip 箭头 | Boolean | — | true |
| close-outside | 是否可以通过点击其他位置 关闭 tooltip | boolean    | — | true |

### Events

| 事件名称           | 说明             | 回调参数                                     |
| -------------- | -------------- | ---------------------------------------- |
| show     |显示时触发       | - |
| hide | 隐藏时触发 | - |
| menu-click | menu 模式下点击某一选项触发 | 当前选项内容{name,content}|

### Slot

| name      | 说明       |
|------------- |----------- |
| content | 多行内容或用户自定义样式 |

### Tooltip 外部样式类

| 类名     | 说明                |
|---------|---------------------|
| custom-class | 根结点样式 |
| custom-arrow | 尖角样式 |
| custom-pop | 文字提示样式 |
