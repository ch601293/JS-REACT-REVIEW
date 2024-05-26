## js隐式类型转换问题

## 数学运算符中的类型转换

**我们在对各种非`Number`类型运用数学运算符(`- \* /`)时，会先将非`Number`类型转换为`Number`类型。**

```js
1 - true // 0， 首先把 true 转换为数字 1， 然后执行 1 - 1
1 - null // 1,  首先把 null 转换为数字 0， 然后执行 1 - 0
1 * undefined //  NaN, undefined 转换为数字是 NaN
2 * ['5'] //  10， ['5']首先会变成 '5', 然后再变成数字 5
```

### 加法的特殊性

- 当一侧为`String`类型，被识别为字符串拼接，并会优先将另一侧转换为字符串类型。
- 当一侧为`Number`类型，另一侧为原始类型，则将原始类型转换为`Number`类型。
- 当一侧为`Number`类型，另一侧为引用类型，将引用类型和`Number`类型转换成字符串后拼接。

## 逻辑语句中的类型转换

### 1.单个变量

只有 `null` `undefined` `''` `NaN` `0` `false` 这几个是 `false`，其他的情况都是 `true`，比如 `{}` , `[]`。

### 2.使用 == 比较中的5条规则

- 规则 1：`NaN`和其他任何类型比较永远返回`false`（包括和他自己）。
- 规则 2：Boolean 和其他任何类型比较，Boolean 首先被转换为 Number 类型。

```js
true == 1  // true 
true == '2'  // false, 先把 true 变成 1，而不是把 '2' 变成 true
true == ['1']  // true, 先把 true 变成 1， ['1']拆箱成 '1', 再参考规则3
true == ['2']  // false, 同上
undefined == false // false ，首先 false 变成 0，然后参考规则4
null == false // false，同上
```

- 规则 3：`String`和`Number`比较，先将`String`转换为`Number`类型。

- 规则 4：`null == undefined`比较结果是`true`，除此之外，`null`、`undefined`和其他任何结果的比较值都为`false`。

- `原始类型`和`引用类型`做比较时，引用类型会依照`ToPrimitive`规则转换为原始类型。

  ⭐️`ToPrimitive`规则，是引用类型向原始类型转变的规则，它遵循先`valueOf`后`toString`的模式期望得到一个原始类型。