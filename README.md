
## nigo-vue-pagination v1.0.0
`    npm install nigo-vue-pagination
`

`    yarn add nigo-vue-pagination
`
## 使用示例
`    import Pagination from 'nigo-vue-pagination'
`
```
  <Pagination         :page-total="873"
                      :page-num="7"
                      :page-size="8"
                      :color="color"
                      @currentCallBack="currentCallBack"

></Pagination>

```
## props
| 参数 | 说明 | 类型 | 默认值 |
| :---| :--- | :--- | :--- |
| page-total | 总数据 | Number | 100 |
| page-num | 要显示页数 | Number | 10 |
| page-size | 分页大小 | Number | 5 |
| color | 传入的主题颜色 | Number | #409eff |
| currentCallBack | 返回点击的当前索引值 | Events |  |




  
 ### Keywords
vue 、JavaScript 、drag
