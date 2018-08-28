#  数据规范

<h3 id="path">1、接口路径组成</h3>

建议以统一字符标识开头。 例如：**/api/user/list**，统一前缀的作用是方便以后分开部署时配置nginx转发规则。

<h3 id="response">2、返回值参数规范</h3>

```js
{
  "status": 0, // 业务状态 (0：业务请求成功；5：未登录；其他为特定业务错误)
  "msg": "用户名密码错误", //业务处理错误消息
  "data": {
    list:[], //列表数据
    pageNo:1, //页码
    pageSize:10, //页大小
    total:50 // 总记录条数
  }
}
```

<h3 id="menu">3、左侧导航栏菜单数据格式</h3>

```js
// 从服务器获取方式
{
  "status": 0, // 业务状态 (0：业务请求成功；5：未登录；其他为特定业务错误)
  "msg": "", // 业务处理错误消息
  "data": [{
    "id": "026001",
    "name": "Dashboard",
    "url": "/dashboard",
    "extra": "laptop",
    "children": []
  },
  {
    "id": "026002",
    "name": "应用管理",
    "url": null,
    "extra": "cloud-download-o",
    "children": [{
        "id": "026002004",
        "name": "应用列表",
        "url": "/application/list",
        "extra": null,
        "children": []
    }]
  },
  {
    "id": "026003",
    "name": "运维管理",
    "url": null,
    "extra": "customer-service",
    "children": [{
        "id": "026003001",
        "name": "机器列表",
        "url": "/machine/list",
        "extra": null,
        "children": []
    }]
  }
]}

// json方式(请选择数据源类型为json)
[
  {
    "id": "026001",
    "name": "Dashboard",
    "url": "/dashboard",
    "extra": "laptop",
    "children": []
  },
  {
    "id": "026002",
    "name": "应用管理",
    "url": null,
    "extra": "cloud-download-o",
    "children": [{
        "id": "026002004",
        "name": "应用列表",
        "url": "/application/list",
        "extra": null,
        "children": []
    }]
  },
  {
    "id": "026003",
    "name": "运维管理",
    "url": null,
    "extra": "customer-service",
    "children": [{
        "id": "026003001",
        "name": "机器列表",
        "url": "/machine/list",
        "extra": null,
        "children": []
    }]
  }
]
```
<h3 id="tree">4、树形控件数据格式</h3>

文件夹、组织架构、生物分类、国家地区等等，世间万物的大多数结构都是树形结构。使用树控件可以完整展现其中的层级关系，并具有展开收起选择等交互功能。

```js
{
  status: 0, // 业务状态 (0：业务请求成功；5：未登录；其他为特定业务错误)
  msg: '', // 业务处理错误消息
  data: [{
    title: '0-0',
    key: '0-0',
    children: [{
      title: '0-0-0',
      key: '0-0-0',
      children: [
        { title: '0-0-0-0', key: '0-0-0-0' },
        { title: '0-0-0-1', key: '0-0-0-1' },
        {
            title: '0-0-0-2',
            key: '0-0-0-2',
            checked: true,  //默认选中
            disabled: true //默认不可用
        }
      ]
    }, {
      title: '0-0-1',
      key: '0-0-1',
      children: [
        { title: '0-0-1-0', key: '0-0-1-0' },
        { title: '0-0-1-1', key: '0-0-1-1' },
        { title: '0-0-1-2', key: '0-0-1-2' }
      ]
    }, {
      title: '0-0-2',
      key: '0-0-2'
    }]
  }, {
    title: '0-1',
    key: '0-1',
    children: [
      { title: '0-1-0-0', key: '0-1-0-0' },
      { title: '0-1-0-1', key: '0-1-0-1' },
      { title: '0-1-0-2', key: '0-1-0-2' }
    ]
  }, {
    title: '0-2',
    key: '0-2'
  }]
}
```

<h3 id="axis">5、折线图、条形图、柱状图数据格式</h3>

后台返回的数据格式可能有多种，为了满足不同的格式，我们模拟了可能的几种情况，如下：

```js
//1、re返回的数据格式是JSON对象，数据内容是动态的
{
  "status": 0,
  "data": {
    "re": {
      "time": ["2017-01-03 00:00", "2017-01-03 00:05", "2017-01-03 00:10", "2017-01-03 00:15", "2017-01-03 00:20", "2017-01-03 00:25"],
      "detail":{
        "total": [487, 702, 768, 337, 411, 1869],
        "expires": [182, 234, 290, 104, 131, 630],
        "expired": [183, 230, 208, 109, 139, 639],
        "evicted": [122, 238, 270, 124, 141, 600]
      }
    }
  }
}
//动态的第二种情况
{
  "status": 0,
  "data": {
    "re": {
      "time": [
        "2017-01-03 00:00",
        "2017-01-03 00:05",
        "2017-01-03 00:10",
        "2017-01-04 00:10",
        "2017-01-05 00:10"
      ],
      "detail": {
        "total": {
          "title": "总数",
          "value": [
            487,
            702,
            768,
            337,
            411,
            1869
          ],
          "type": "bar",
          "selected": true,
          "yAxisIndex": 0
        },
        "expires": {
          "title": "有效",
          "selected": true,
          "value": [
            287,
            502,
            268,
            537,
            411,
            1869
          ],
          "type": "line"
        },
        "expired": {
          "title": "过期数",
          "selected": true,
          "value": [
            187,
            702,
            568,
            337,
            611,
            1869
          ],
          "type": "bar"
        }
      }
    }
  }
}
//2、和上面的类似，但是数据内容是可以逐条添加的
{
  "status": 0,
  "data": {
    "re": {
      "time": ["2017-01-03 00:00", "2017-01-03 00:05", "2017-01-03 00:10", "2017-01-03 00:15", "2017-01-03 00:20", "2017-01-03 00:25"], 
      "total": [487, 702, 768, 337, 411, 1869],
      "expires": [182, 234, 290, 104, 131, 630],
      "expired": [183, 230, 208, 109, 139, 639],
      "evicted": [122, 238, 270, 124, 141, 600]
    }
  }
}
//3、re返回的是数组，这个需要我们的内部逻辑去转换为可用的格式
{
  "status": 0,
  "data": {
    "re": [{
      "time": ["2017-01-03 00:00"],
      "total": 487,
      "expires": 182,
      "expired": 183,
      "evicted": 222
    },{
      "time": ["2017-01-03 00:05"],
      "total": 387,
      "expires": 282,
      "expired": 1583,
      "evicted": 522
    },{
      "time": ["2017-01-03 00:10"],
      "total": 587,
      "expires": 482,
      "expired": 983,
      "evicted": 122
    }]
  }
}
```
<h3 id="pie">6、饼图/环形图、漏斗图数据格式</h3>

我们把饼图和环形图集成在了一起，当只配置一项时会渲染出饼图，配置两项时渲染成环形图，如下：

```js
//1、支持单条添加数据，每增加一个条目即增加一个扇形区域（漏斗图同理）
{
  "status": 0,
  "data": {
    "re": {
      "猛禽": "335",
      "雅阁": "310",
      "帕萨特": "234",
      "蒙迪欧": "135",
      "CR-V": "1048",
      "森林人": "251",
      "RAV-4": "147",           
      "哈弗": "102"               
    }
  }
}
//2、动态数据，分别给出内环和外环的数据，只配置一项时为饼图
{
  "status": 0,
  "data": {      
    "re": {
      "inner": {
        "皮卡": 335,
        "轿车": 679,
        "SUV": 1548
      },
      "outer": {
        "猛禽": "335",
        "雅阁": "310",
        "帕萨特": "234",
        "蒙迪欧": "135",
        "CR-V": "1048",
        "森林人": "251",
        "RAV-4": "147",           
        "哈弗": "102"    
      }
    }
  }
}
```
<h3 id="point">7、散点图数据格式</h3>

散点图虽然也属于直角坐标系图形，但是数据格式比较特殊，因为每一个点的确定都需要一组坐标，每一系列都需要有x轴和y轴的数据，示例数据如下：

```js
{
  "status": 0,
  "data": {
    "re": {
      "male": {
        "xAxis": [165.1, 170.4, 178.2, 185.5, 190.2],
        "yAxis": [55.2, 66.3, 77.4, 88.5, 99.6]
      },
      "female": {
        "xAxis": [155.1, 160.4, 168.2, 175.5, 180.2],
        "yAxis": [45.2, 56.3, 67.4, 78.5, 89.6]               
      }
    }
  }
}
```
<h3 id="radar">8、雷达图数据格式</h3>

```js
{
  "status": 0,
  "data": {
    "re": {
      "indicator": ["ucar", "fcar", "mmc", "zuche", "coffee"],
      "budget": [2000, 10000, 500, 60000, 8900],
      "expense": [2500, 10500, 1000, 65000, 10000]     
    }       
  }
}
```
<h3 id="treeChart">9、树图数据格式</h3>

树图在展示具有多层包含关系的逻辑时非常直观易懂，示例数据如下：

```js
{
  "status": 0,
  "data": {
    "re": {
      "name": "flare",
      "children": [{
        "name": "analytics",
        "children": [
          {
            "name": "cluster",
            "children": [
              {"name": "AgglomerativeCluster", "value": 3938},
              {"name": "CommunityStructure", "value": 3812},
              {"name": "HierarchicalCluster", "value": 6714},
              {"name": "MergeEdge", "value": 743}
            ]
          },
          {
            "name": "graph",
            "children": [
              {"name": "BetweennessCentrality", "value": 3534},
              {"name": "LinkDistance", "value": 5731},
              {"name": "MaxFlowMinCut", "value": 7840},
              {"name": "ShortestPaths", "value": 5914},
              {"name": "SpanningTree", "value": 3416}
            ]
          },
          {
            "name": "optimization",
            "children": [
              {"name": "AspectRatioBanker", "value": 7074}
            ]
          }
        ]
      }]
    }
  }
}
```
<h3 id="auth">10、权限控制数据格式</h3>

开发者可以在接口中返回当前用户拥有的权限code列表，例如 ['00001','000002',...]，每个code对应页面上指定的组件元素。

```js
{
  "status": 0,
  "msg": "", //业务处理错误消息
  "data": {
    authCode:['00001','000002'], //权限列表
  } 
}
```
<h3 id="heatMap">11、热力图数据格式</h3>

需要自行提供百度地图api，echarts根据百度地图扩展出热力图。

```js
[
  [{
    coord: [120.08094825523, 30.242275513241],  // 坐标字段
    elevation: 81,  // 业务字段
  }, {
    coord: [120.08055098063, 30.242746889455],
    elevation: 107.5,
  }, {
    coord: [120.08091800677, 30.243117337651],
    elevation: 107,
  }],
  [{
    coord: [120.14340405029, 30.253692727708],
    elevation: 21,
  }, {
    coord: [120.14337970209, 30.253859682295],
    elevation: 29,
  }, {
    coord: [120.14328651034, 30.254070236173],
    elevation: 29,
  }],
  [{
    coord: [120.11896546528, 30.20202369587],
    elevation: 125.1,
  }, {
    coord: [120.12023038701, 30.202136996865],
    elevation: 125.1,
  }, {
    coord: [120.1200956896, 30.202256331222],
    elevation: 125.1,
  }],
]
```
<div style="text-align:right; font-weight:bold;margin-top:50px;">
  <a href="./publish" style="margin-right:20px">← 应用部署</a>
</div>
