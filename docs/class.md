<h1 id="class">样式视图</h1>
   为了满足自定义外观的需求，我们在每个页面的基础上新增了外观视图，用来改变当前页面组件的外观。  

### 1. 如何添加  {docsify-ignore}  

（1）在div的容器上填写class类名，例如填写box，那么当前容器就具有了box的样式类名  
（2）样式视图中添加外观样式
  
  实例代码片段

  ```css
  .box {
    border:solid 1px red;
    background:#ccc;
    .ant-btn {
      backckground:#000;
      color:#fff;
      &:hover {
        baclground:rgba(0,0,0,.8);
      }
    }
  }
  ```
### 2. 样式作用域 {docsify-ignore}
  页面的样式视图添加的自定义样式规则仅作用于当前页面，不会影响其他页面的外观。
  

