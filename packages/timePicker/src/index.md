---
title: 时间组件
nav:
  title: 时间组件
  path: /components
  order: 1
group:
  title: timepicker
  path: /timepicker
---

## TimePicker 时间选择框

当用户需要输入一个时间，可以点击标准输入框，弹出时间面板进行选择。  
主要区别于 antd 的一个区别就是 antd 时间选择是从 00:00 - 23:59, 而在一些项目中要求使用的是 00:01 - 24:00

### 代码演示

### 基本

```tsx
/**
 * title: 基本
 * desc: 点击`TimePicker`然后可以在浮层中选择或者输入某一时间。
 */
import React from 'react';
import { TimePicker } from '@sunny/timepicker';

export default () => {
  return <TimePicker />;
};
```

```tsx
/**
 * title: defaultValue
 * desc: 默认的defaultValue
 */
import React from 'react';
import { TimePicker } from '@sunny/timepicker';

export default () => {
  return <TimePicker defaultValue={'12:05'} />;
};
```

### 受控组件

```tsx
/**
 * title: 受控组件
 * desc: 其中`value` 和 `onChange` 需要配合使用。
 */
import React, { useState } from 'react';
import { TimePicker } from '@sunny/timepicker';
import type { Moment } from 'moment';

export default () => {
  const [value, setValue] = useState<string>('12:00');
  return (
    <TimePicker
      value={value}
      onChange={(timeString: string) => {
        setValue(timeString);
      }}
    />
  );
};
```

### 禁用

```tsx
/**
 * title: 禁用
 * desc: 禁用时间选择。
 */
import React, { useState } from 'react';
import { TimePicker } from '@sunny/timepicker';
import type { Moment } from 'moment';

export default () => {
  const [value, setValue] = useState<string>('12:00');
  return (
    <TimePicker
      value={value}
      disabled
      onChange={(_time: Moment, timeString: string) => {
        setValue(timeString);
      }}
    />
  );
};
```

### 步长选项

```tsx
/**
 * title: 步长选项
 * desc: 可以使用 `hourStep` `minuteStep` 按步长展示可选的时分秒。
 */
import React, { useState } from 'react';
import { TimePicker } from '@sunny/timepicker';
import type { Moment } from 'moment';

export default () => {
  const [value, setValue] = useState<string>('12:00');
  return (
    <TimePicker
      value={value}
      hourStep={2}
      minuteStep={5}
      onChange={(_time: Moment, timeString: string) => {
        setValue(timeString);
      }}
    />
  );
};
```

### 禁止选择部分

```tsx
/**
 * title: 禁止选择部分
 * desc: 可以使用 `disabledHours` `disabledMinutes` 禁止选择部分选项
 */
import React, { useState } from 'react';
import { TimePicker } from '@sunny/timepicker';
import type { Moment } from 'moment';

export default () => {
  const [value, setValue] = useState<string>('12:00');
  return (
    <TimePicker
      value={value}
      disabledHours={() => {
        return [0, 1, 2];
      }}
      disabledMinutes={(selectedHour: number | null) => {
        if (selectedHour === 5 || selectedHour === 7 || selectedHour === 9) {
          return [30, 15];
        }
      }}
      minuteStep={15}
      onChange={(_time: Moment, timeString: string) => {
        setValue(timeString);
      }}
    />
  );
};
```

### API

`<TimePicker />` | 参数 | 说明 | 类型 | 默认值 | | :---- | :----: | :----: | :----: | | className | 赋值给整个组件的 className | string | - | | value | 当前时间 | string | null | null | | width | 整个 TimePicker 的宽度 | number | 120 | | disabled | 禁用全部操作 | boolean | false | | disabledHours | 禁止选择部分小时选项 | function(): void | - | | disabledMinutes | 禁止选择部分分钟选项 | function(selectedHour: number): void | - | | minuteStep | 分钟选项间隔 | number | 1 | | hourStep | 小时选项间隔 | number | 1 | | onChange | 时间发生变化的回调 | function(timeString: string): void | - |

### FAQ

TODO:  
一周：

1. 缺少组件内校验
2. 缺少 defaultValue

二周：

1. 弹出收起样式时间过渡
2. '此时'功能有待优化（存在步长时选择此时）

三周：

1. 时间选完以后会回到初始位置，体验不好
2. 增加秒选项(这个可能需要的时间更长一些)

后续有思路优化：

1. 时间复选多组件校验
