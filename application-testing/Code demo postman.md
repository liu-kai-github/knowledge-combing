## postman代码测试的应用

### postman基础

* postman响应的基本规则

```
tests['true'] = true;  // true
tests['false'] = false;  // false
tests['!运算符'] = !false;  // true
tests['字符串'] = 'string';  // true
tests['空字符串'] = '';  // false
tests['数字0'] = 0;  // false
tests['数字大于0'] = 1;  // true
tests['数字小于0'] = -1;  // true
tests['null'] = null;  // false
tests['undefind'] = undefined;  // false
```

* 响应内容是否包含哪些字符

```
tests["Body matches string"] = responseBody.has("string_you_want_to_search");
```

* 响应体数据的详细检查

```
var jsonData = JSON.parse(responseBody);
tests["Your test name"] = jsonData.value === 100;
```

* 响应头的详细检查

```
tests["Content-Type is present"] = postman.getResponseHeader("Content-Type");
```

* 响应时间的检查

```
tests["Response time is less than 200ms"] = responseTime < 200;
```

* http响应码检查

```
tests["Status code is 200"] = responseCode.code === 200;
```

* 测试通用模板

```
if(responseCode.code === 200) {
    tests['状态码为200'] = true;
    tests[`本次响应时间为${responseTime}毫秒，小于200毫秒`] = responseTime < 200;
    tests['响应数据类型为 application/json'] = postman.getResponseHeader("Content-Type") === 'application/json';
} else {
    throw new Error(`状态码为${responseCode.code}，无法继续判断`);
}

//需求逻辑判断

```

### 实例

* 测试 ``http://wxtest.xw18.cn/basedata/get_city_by_code?code=4403`` 接口

```
if(responseCode.code === 200) {
    tests['状态码为200'] = true;
    tests[`本次响应时间为${responseTime}毫秒，小于200毫秒`] = responseTime < 200;
    tests['响应数据类型为 application/json'] = postman.getResponseHeader("Content-Type") === 'application/json';
} else {
    throw new Error(`状态码为${responseCode.code}，无法继续判断`);
}

//需求逻辑判断
const jsonData = JSON.parse(responseBody);
if (jsonData.code === 0) {
    tests['后台已正确响应'] = true;
    const testData = jsonData.data;
    tests['code为4403'] = testData.code === 4403;
    tests['name为深圳'] = testData.name === '深圳';
} else {
    tests['后台未正确响应']
}
```

* 测试 ``http://wxtest.xw18.cn/producelist?featured=1&page_no=0&page_size=10&shop_id=13439``

```
if(responseCode.code === 200) {
    tests['状态码为200'] = true;
    tests[`本次响应时间为${responseTime}毫秒，小于200毫秒`] = responseTime < 200;
    tests['响应数据类型为 application/json'] = postman.getResponseHeader("Content-Type") === 'application/json';
} else {
    throw new Error(`状态码为${responseCode.code}，无法继续判断`);
}

const testItem = item => {
    const id = item.id;
    tests[`id为${id}，id存在`] = item.id;
    tests[`id为${id}的商品，name为${item.name}，name存在`] = item.name;
    tests[`id为${id}的商品，price为${item.price}，price存在`] = item.price;
    tests[`id为${id}的商品，price为${item.price}，大于0且小于999999`] = item.price > 0 && item.price < 99999;
}

const jsonData = JSON.parse(responseBody);
if (jsonData.code === 0) {
    tests['后台已正确响应'] = true;
    const testData = jsonData.data.objects;
    tests['返回数据的长度为10'] = testData.length === 10;
    for (const item of testData) {
        testItem(item);
    }
} else {
    tests['后台未正确响应']
}
```











