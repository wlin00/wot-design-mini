## DatetimePicker 日期时间选择器

为 Picker 组件的封装，在其内部构建好日期时间选项。

### 引入

```json
{
  "usingComponents": {
    "wd-datetime-picker": "/wot-design/datetimePicker/index"
  }
}
```

### 基本用法

`value` 设置绑定值，默认为 'datetime' 类型，展示年月日时分，绑定值为 `时间戳` 类型，如果为 'time' 类型，绑定值为字符串。通过绑定 `bind:confirm` 事件获取当前选中的时间，并赋值给绑定的value变量。label 可以不传。可以通过 `label-width` 设置标题宽度，默认为 '33%'。

```html
<wd-datetime-picker value="{{value}}" label="日期选择" bind:confirm="handleConfirm" />
```
```javascript
Page({
  data: {
    value: Date.now(),
  },
  handleConfirm ({ detail }) {
    this.setData({
      value: detail
    })
  }
})
```

### date 类型

'date' 类型只展示年月日。

```html
<wd-datetime-picker type="date" value="{{value}}" label="年月日" />
```
```javascript
Page({
  data: {
    value: Date.now(),
  }
})
```
### year-month 类型

'year-month' 类型只展示年月。

```html
<wd-datetime-picker type="year-month" value="{{value}}" label="年月" />
```
```javascript
Page({
  data: {
    value: Date.now(),
  }
})
```

### time 类型

'time' 类型只展示时分。

```html
<wd-datetime-picker type="time" value="{{value}}" label="时分" />
```
```javascript
Page({
  data: {
    value: Date.now(),
  }
})
```

### 修改展示格式
> 自定义函数必须写在data中

给 `display-format` 属性传入一个函数，接收所有选中项数组，返回展示的文本内容。

```html
<wd-datetime-picker value="{{value}}" label="展示格式" display-format="{{displayFormat}}" />
```
```javascript
Page({
  data: {
    value: new Date(),
    displayFormat (items) {
        return `${items[0].label}年${items[1].label}月${items[2].label}日 ${items[3].label}:${items[4].label}`
    }
  }
})
```
### 修改弹出层内部格式
> 自定义函数必须写在data中

给 `formatter` 属性传入一个函数，接收 `type` 和 `value` 值，返回展示的文本内容。`type` 有 `year`、`month`、`date`、`hour`、`minute` 类型，`value` 为 `number` 类型。
使用自定义`formatter`会关闭内置的默认`display-format`函数。

```html
<wd-datetime-picker value="{{value}}" label="内部格式" formatter="{{formatter}}" />
```
```javascript
Page({
  data: {
    value: new Date(),
    formatter (type, value) {
      switch (type) {
        case 'year':
          return value + '年'
        case 'month':
          return value + '月'
        case 'date':
          return value + '日'
        case 'hour':
          return value + '时'
        case 'minute':
          return value + '分'
        default:
          return value
      }
    }
  }
})
```
### 过滤选项

给 `filter` 属性传入一个函数，接收 `type` 和 `values` 值，返回列的选项列表。`type` 有 `year`、`month`、`date`、`hour`、`minute` 类型，`values` 为 number数组。
> 自定义函数必须写在data中
```html
<wd-datetime-picker value="{{value}}" label="过滤选项" filter="{{filter}}" />
```
```javascript
Page({
  data: {
    value: new Date(),
    filter (type, values) {
      if (type === 'minute') {
        return values.filter(value => value % 5 === 0)
      }
      return values
    }
  }
})
```

### 选择器大小

通过设置 `size` 修改选择器大小，将 `size` 设置为 'large' 时字号为 16px。

```html
<wd-datetime-picker label="日期选择" size="large" value="{{value}}" />
```

### 错误状态

设置 `error` 属性，选择器的值显示为红色。

```html
<wd-datetime-picker label="日期选择" error value="{{value}}" />
```

### 值靠右展示

设置 `align-right` 属性，选择器的值靠右展示。

```html
<wd-datetime-picker label="日期选择" align-right value="{{value}}" />
```

### 确定前校验

设置 `before-confirm` 函数，在用户点击`确定`按钮时，会执行 `before-confirm` 函数，并传入 `value`(time 类型为字符串，其他为时间戳) 、 `resolve` 和 `picker` 参数，可以对 `value` 进行校验，并通过 `resolve` 函数告知组件是否确定通过，`resolve` 接受1个 boolean 值，`resolve(true)` 表示选项通过，`resolve(false)` 表示选项不通过，不通过时不会关闭 `picker`弹窗。可以通过 `picker` 参数直接设置 `loading` 等属性。

```html
<wd-datetime-picker label="before-confirm" value="{{value}}" before-confirm="{{beforeConfirm}}" bind:confirm="handleConfirm" />
```

```javascript
Page({
  data: {
    value: '',
    beforeConfirm: function (value, resolve, picker) {
      picker.setData({
        loading: true
      })
      setTimeout(() => {
        picker.setData({
          loading: false
        })
        if (value > Date.now()) {
          resolve(false)
          Toast.error('不能选择大于今天的日期')
        } else {
          resolve(true)
        }
      }, 2000)
    }
  },
  handleConfirm ({ detail }) {
    this.setData({
      value: detail
    })
  }
})
```

### Attributes

| 参数      | 说明                                 | 类型      | 可选值       | 默认值   |
|---------- |------------------------------------ |---------- |------------- |-------- |
| value | 选中项，当 type 为 time 时，类型为字符串，否则为 Date | string / date | - |
| type | 选择器类型 | string | 'date' / 'year-month' / 'time' | 'datetime' |
| loading | 加载中 | boolean | - | false |
| visible-item-count | 展示的行数 | number | - | 7 |
| item-height | 选项高度 | number | - | 33 |
| title | 弹出层标题 | string | - | - |
| cancel-button-text | 取消按钮文案 | string | - | '取消' |
| confirm-button-text | 确认按钮文案 | string | - | '完成' |
| label | 选择器左侧文案，label可以不传 | string | - | - |
| placeholder | 选择器占位符 | string | - | '请选择' |
| disabled | 禁用 | boolean | - | fasle |
| readonly | 只读 | boolean | - | false |
| display-format | 自定义展示文案的格式化函数，返回一个字符串 | function | - | - |
| formatter | 自定义弹出层选项文案的格式化函数，返回一个字符串 | function | - | - |
| filter | 自定义过滤选项的函数，返回列的选项数组 | function | - | - |
| minDate | 最小日期 | date | - | 当前日期 - 10年 |
| maxDate | 最大日期 | date | - | 当前日志 + 10年 |
| minHour | 最小小时，time类型时生效 | number | - | 0 |
| maxHour | 最大小时，time类型时生效 | number | - | 23 |
| minMinute | 最小分钟，time类型时生效 | number | - | 0 |
| maxMinute | 最大分钟，time类型时生效 | number | - | 59 |
| size | 设置选择器大小 | string | 'large' | - |
| label-width | 设置左侧标题宽度 | string | - | '33%' |
| error | 是否为错误状态，错误状态时右侧内容为红色 | boolean | - | false |
| align-right | 选择器的值靠右展示 | boolean | - | false |
| use-label-slot | label 使用插槽 | boolean | - | false |
| before-confirm | 确定前校验函数，接收 (value, resolve, picker) 参数，通过 resolve 继续执行 picker，resolve 接收1个boolean参数 | function | - | - |

### Events

| 事件名称      | 说明                                 | 参数     |
|------------- |------------------------------------ |--------- |
| bind:confirm | 点击右侧按钮触发 | 当前选中日期的时间戳，'time' 类型则为字符串 |
| bind:cancel | 点击左侧按钮触发 | - |

### Slot

| name      | 说明       |
|------------- |----------- |
| label | 左侧标题插槽 |

### 外部样式类

| 类名     | 说明                |
|---------|---------------------|
| custom-view-class | pickerView 外部自定义样式 |
| custom-label-class | label 外部自定义样式 |
| custom-value-class | value 外部自定义样式 |
