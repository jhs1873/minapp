<!-- https://developers.weixin.qq.com/miniprogram/dev/component/picker-view.html -->

#### picker-view

嵌入页面的滚动选择器

  属性名            |  类型          |  说明                                                                                                                          | 最低版本 
--------------------|----------------|--------------------------------------------------------------------------------------------------------------------------------|----------
  value             |  NumberArray   |数组中的数字依次表示 picker-view 内的 picker-view-colume 选择的第几项（下标从 0 开始），数字大于 picker-view-column 可选项长度时，选择最后一项。|          
  indicator-style   |  String        |  设置选择器中间选中框的样式                                                                                                    |          
  indicator-class   |  String        |  设置选择器中间选中框的类名                                                                                                    |  1.1.0   
  mask-style        |  String        |  设置蒙层的样式                                                                                                                |  1.5.0   
  mask-class        |  String        |  设置蒙层的类名                                                                                                                |  1.5.0   
  bindchange        |  EventHandle   |当滚动选择，value 改变时触发 change 事件，event.detail = {value: value}；value为数组，表示 picker-view 内的 picker-view-column 当前选择的是第几项（下标从 0 开始）|          

**注意**：其中只可放置`<picker-view-column/>`组件，其他节点不会显示。

#### picker-view-column

仅可放置于`<picker-view />`中，其孩子节点的高度会自动设置成与picker-view的选中框的高度一致

**示例代码：**

    <view>
      <view>{{year}}年{{month}}月{{day}}日</view>
      <picker-view indicator-style="height: 50px;" style="width: 100%; height: 300px;" value="{{value}}" bindchange="bindChange">
        <picker-view-column>
          <view wx:for="{{years}}" style="line-height: 50px">{{item}}年</view>
        </picker-view-column>
        <picker-view-column>
          <view wx:for="{{months}}" style="line-height: 50px">{{item}}月</view>
        </picker-view-column>
        <picker-view-column>
          <view wx:for="{{days}}" style="line-height: 50px">{{item}}日</view>
        </picker-view-column>
      </picker-view>
    </view>
    

    const date = new Date()
    const years = []
    const months = []
    const days = []
    
    for (let i = 1990; i <= date.getFullYear(); i++) {
      years.push(i)
    }
    
    for (let i = 1 ; i <= 12; i++) {
      months.push(i)
    }
    
    for (let i = 1 ; i <= 31; i++) {
      days.push(i)
    }
    
    Page({
      data: {
        years: years,
        year: date.getFullYear(),
        months: months,
        month: 2,
        days: days,
        day: 2,
        year: date.getFullYear(),
        value: [9999, 1, 1],
      },
      bindChange: function(e) {
        const val = e.detail.value
        this.setData({
          year: this.data.years[val[0]],
          month: this.data.months[val[1]],
          day: this.data.days[val[2]]
        })
      }
    })
    

![picker_view](https://mp.weixin.qq.com/debug/wxadoc/dev/image/picker_view.png?t=201838)

##### Tips：

1.  `tip`: 滚动时在iOS自带振动反馈，可在系统设置 -> 声音与触感 -> 系统触感反馈中关闭
