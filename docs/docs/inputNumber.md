## InputNumber 计数器

### 引入

```json
{
  "usingComponents": {
    "wd-input-number": "/wot-design/inputNumber/index"
  }
}
```

### 基本用法

通过监听 `change` 事件获取`value`变化后的值。

```html
<wd-input-number value="{{ value }}" bind:change="handleChange" />

Page({
  data: {
    value: 1
  },
  handleChange ({ detail }) {
    this.setData({
      value: detail
    })
  }
})
```

### 设置步长

设置 `step` 步长，即每次value变化的绝对值。

```html
<wd-input-number value="{{ value }}" bind:change="handleChange" step="{{ 2 }}" />
```

### 设置最小最大值

设置 `min` 最小值，`max` 最大值。`min` 默认为1。

```html
<wd-input-number value="{{ value }}" bind:change="handleChange" min="{{ 3 }}" max="{{ 10 }}" />
```

### 禁用

设置 `disabled` 属性。

```html
<wd-input-number value="{{ value }}" bind:change="handleChange" disabled />
```

### 无输入框

设置 `without-input` ，不展示输入框。

```html
<wd-input-number value="{{ value }}" bind:change="handleChange" without-input />
```

### 设置小数精度

设置 `precision` 属性，默认为0。

```html
<wd-input-number value="{{ value }}" bind:change="handleChange" precision="{{ 2 }}" step="{{ 0.1 }}" />
```

### 严格步数倍数

设置 `step-strictly` 属性，强制输入框输入内容为 `step` 的倍数（当用户输入完成后触发change时，会更正输入框内容）。

```html
<wd-input-number value="{{ value }}" bind:change="handleChange" step-strictly step="{{ 2 }}" />
```

### 修改输入框宽度

设置 `input-width` 设置宽度，该值接受1个字符串，可以是表示尺寸的任何单位。

```html
<wd-input-number value="{{ value }}" bind:change="handleChange" input-width="70px" />
```

### Attributes

| 参数      | 说明                                 | 类型      | 可选值       | 默认值   |
|---------- |------------------------------------ |---------- |------------- |-------- |
| value | 绑定值 | number / string | - | - |
| min | 最小值 | number | - | 1 |
| max | 最大值 | number | - | Infinity |
| step | 步数 | number | - | 1 |
| step-strictly | 严格值为步数的倍数 | boolean | - | false |
| precision | 小数精度 | number | - | 0 |
| disabled | 禁用 | boolean | - | false |
| without-input | 不显示输入框 | boolean | - | false |
| input-width | 输入框宽度 | string | - | 36px |

### Events

| 事件名称      | 说明                                 | 参数     |
|------------- |------------------------------------ |--------- |
| bind:change | 值修改事件 | event.detail = value,value为当前值 |
| bind:focus | 输入框获取焦点事件 | - |
| bind:blur | 输入框失去焦点事件 | event.detail = value,value为当前值 |

### 外部样式类

| 类名     | 说明                |
|---------|---------------------|
| custom-class | 根结点样式 |
