# 方法及工具类

## 1.全局方法

在系统的实际运行过程中有很多需要和用户行为交互的情况，为了处理这些灵活多变的场景，我们允许开发者添加自定义代码片段。而且，我们还在每个需要自定义代码的地方额外集成了一些全局可用的方法供开发者调用，以下为可调用代码说明。

### this.setState(object) {docsify-ignore}
  改变页面state变量值  
  • <span class="token keyword">object</span> {object} 变量对象
```js
  this.setState({
    userName:'vdp',
  });
```

### this.getDsData(name) {docsify-ignore}
  获取指定数据源返回的数据，带完整状态等信息。  
  • <span class="token keyword">name</span> {string} 数据源名称
```js
  const data = this.getDsData("测试数据源");
  if (data && !data.status) {
    console.log(data.data);
  }
```
### this.getFormValues(name, fieldName, isToQueryString) {docsify-ignore}
  获取指定表单收集的数据  
  • <span class="token keyword">name</span> {array} 表单名称集合  
  • <span class="token keyword">fieldName</span> {string} 字段名称，若不指定则获取所有字段值  
  • <span class="token keyword">isToQueryString</span> {boolean} 是否转换为url参数形式
```js
  // 如果有一些场景，默认表单传递的值不能满足后台解析需要，可添加自定义代码，先获取表单值，做处理以后传递给变量
  const formValues  = this.getFormValues(['表单1', '表单2']);
  map(formValues,(v) => {
    return `${v}`;
  });
  this.submitFormValues =  {
    ...formValues,
  };
  const queryString  = this.getFormValues(['表单1','表单2'], null, true);
```
### this.setFormValues(name, object) {docsify-ignore}
  设置指定表单数据  
  • <span class="token keyword">name</span> {string, array} 表单名称集合  
  • <span class="token keyword">object</span> {object} 填充的数据对象
```js
  // 设置表单值demo
  this.setFormValues(['表单1','表单2'],{
    username:'gyd',
    password:'1111',
  });
```
### this.isEdit() {docsify-ignore}
  判断当前页面是否处于修改状态，以填充表单动作作为判断依据。  
```js
  // 弹窗的标题根据状态展示
  const isEdit =  this.isEdit();
  return isEdit ? "修改用户" : "添加用户";
```

## 2.工具类(util)

### util.getViewHeight() {docsify-ignore}
  获取当前浏览器可视区高度
```js
  const clientHeight = util.getViewHeight();
  console.log(clientHeight);
```

### util.getViewWidth() {docsify-ignore}
  获取当前浏览器可视区宽度
```js
  const clientWidth = util.getViewWidth();
  console.log(clientWidth);
```
### util.getUrlParams() {docsify-ignore}
  获取地址栏参数  
  • <span class="token keyword">return</span> {object} 变量对象
```js
  const params = util.getUrlParams();
  console.log(params);
```
### util.getParam(string) {docsify-ignore}  
  获取地址栏指定参数名称  
  • <span class="token keyword">string</span> {string} 参数名称
```js
  const userId = util.getParam('userId');
  console.log(userId);
```
### util.cookie(name, value, options) {docsify-ignore}  
  读写cookie  
  • <span class="token keyword">name</span> {string} cookie键值  
  • <span class="token keyword">value</span> {string} cookie值  
  • <span class="token keyword">options</span> {object} cookie选项设置  
```js
  // 读cookie  
  const userInfo = util.cookie('vdp');
  console.log(userInfo);
  // 写cookie
  util.cookie('vdp','xxx', {
    path:'/',
  });
```
## 3.异步请求处理类

### qs.get(url, params) {docsify-ignore}
  发送一个get请求  
  • <span class="token keyword">url</span> {string} 请求的url地址  
  • <span class="token keyword">params</span> {object} 请求的参数值    
```js
  qs.get('/api/user/list',{
    userId:'1',
  }).then((data)=>{
    console.log(data);
  });
```

### qs.post(url, params) {docsify-ignore}
  发送一个post请求  
  • <span class="token keyword">url</span> {string} 请求的url地址  
  • <span class="token keyword">params</span> {object} 请求的参数值  
```js
  qs.post('/api/user/list',{
    userId:'1',
  }).then((data)=>{
    console.log(data);
  });
```
## 4.日期处理类(moment)
  详细使用请参考moment官网文档 

```js
  const d  = moment(new Date()).format('YYYY-MM-DD');
  console.log(d);
```
## 5.antd组件类
  详细使用请参考antd官网文档 

```js
  const {Icon,Button} = antd;
  return (
    <Button icon={<Icon type ='mail' />}>测试按钮</Button>
  );
```