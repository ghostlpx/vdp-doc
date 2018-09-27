# 权限控制 
 VPD可以将权限控制到任何一个可编辑组件，只要配置相应的权限编码即可完成
### 1. 权限CODE编码 {docsify-ignore}

VDP设计中，CODE编码是通过后端在登录接口中返回，数据KEY指定为“authCode"  
```
{
  status:0,
  msg:'',
  data:{
    authCode:'10000,20000,20001'
  }
}
```
### 2. 权限编码配置 {docsify-ignore}
  在各个组件的权限配置中填写相应模块功能的权限编码
