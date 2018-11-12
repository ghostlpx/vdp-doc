<h1 id="event">多入口共享页面</h1>
  我们在设计页面的时候，存在这样的需求，页面完全相同，只是列表数据不同，数据通过参数来区分，如果做多个页面，显然是很浪费的。  
  因此我们通过共享页面来处理这种场景，根据不同的业务线，列表展示数据不同，可以按照以下步骤配置：

### 1. 共享页面设置步骤 {docsify-ignore}
  （1）新建页面的的时候，页面路径后边带上参数 
  例如：   /lable/data/delimit?1,2,3  
  （2）框架会将此配置解析为以下路径，这三个路径共享同一个页面  
    &ensp;&ensp;&ensp;&ensp; /lable/data/delimit/1  
    &ensp;&ensp;&ensp;&ensp; /lable/data/delimit/2  
    &ensp;&ensp;&ensp;&ensp; /lable/data/delimit/3  
    &ensp;&ensp;&ensp;&ensp; 以上路径对应到同一个页面，数据会根据请求的参数做处理

  （3）菜单配置中添加菜单路径，同时附带上请求的参数  
    &ensp;&ensp;&ensp;&ensp; /lable/data/delimit/1?p=1  
    &ensp;&ensp;&ensp;&ensp; /lable/data/delimit/1?p=2  
    &ensp;&ensp;&ensp;&ensp; /lable/data/delimit/1?p=3  

  （4）在页面中的表格数据获取请求中，勾选附加url参数，这样初始化请求会在获取数据的同时传递页面对应的参数 

### 2. 多层设置 {docsify-ignore}
共享页面允许多层设置  
例如：   /lable/data/delimit?1,2,3&4,5,6
生成页面路径如下:  
 /lable/data/delimit/1/4  
  /lable/data/delimit/1/5  
  /lable/data/delimit/1/6  
  /lable/data/delimit/2/4  
  /lable/data/delimit/2/5  
  /lable/data/delimit/2/6   
  /lable/data/delimit/3/4  
  /lable/data/delimit/3/5  
  /lable/data/delimit/3/6  







