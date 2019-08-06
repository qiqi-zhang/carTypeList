


var cL = require('carList/carList.js')

data:{
    carType: "请选择出行",
    success: false,
    multiArray: [],
    multiIndex: [0, 0, 0],
},

onload:function(){
    var arr = [];
    arr.push(cL.carport);
    arr.push(cL.brands[cL.carport[0]]);
    var k = ['红色', '绿色', '蓝色', '黑色', '粉色', '白色'];
    arr.push(k);
    console.log(arr)
    this.setData({
      multiArray: arr
    })
},


  // 选择车型start
  bindMultiPickerChange: function(e) {
    console.log('picker发送选择改变，携带值为', e.detail.value)
    this.setData({
      multiIndex: e.detail.value
    })
  },
  bindMultiPickerColumnChange: function(e) {
    console.log('修改的列为', e.detail.column, '，值为', e.detail.value);
    var multiArray = this.data.multiArray;
    var a = multiArray[0];

    switch (e.detail.column) {
      case 0:
        var b = cL.brands[cL.carport[e.detail.value]];
        var c = multiArray[2];
        var multiArray = [];

        multiArray.push(a);
        multiArray.push(b);
        multiArray.push(c);

        console.log(multiArray)
        break;
      case 1:
        break;
    }
    var data = {
      multiArray: multiArray,
      multiIndex: this.data.multiIndex,
      carType: '',
      cartype: this.data.multiArray[0][this.data.multiIndex[0]] + "/" + this.data.multiArray[1][this.data.multiIndex[1]] + "/" + this.data.multiArray[2][this.data.multiIndex[2]]
    };
    data.multiIndex[e.detail.column] = e.detail.value;
    this.setData(data);
  },
  // 选择车型end
  
  
  
      <!-- html部分 -->    
      <!-- 车型选择 -->
      <view class='flexrow jc_sb input pl22 pr24 mb28'>
        <view class='color666 font26' style='flex:1;'>车型
          <span class='font22'>（非必选项）：</span>
        </view>
        <view class="section" style='flex:1'>
          <picker mode="multiSelector" bindchange="bindMultiPickerChange" bindcolumnchange="bindMultiPickerColumnChange" value="{{multiIndex}}" range="{{multiArray}}">
            <view wx:if='{{carType=="请选择出行"}}' class='font26 {{carType=="请选择出行" ? "color999":"color333"}}' bindchange="bindMultiPickerChange" style='text-align:right;' bindcolumnchange="bindMultiPickerColumnChange">请选择出行</view>
            <view class="picker font26 color333" style='text-align:right;' wx:else>
              <!-- {{multiArray[0][multiIndex[0]]}}， -->
              {{multiArray[1][multiIndex[1]]}}
              <span class='font22'>({{multiArray[2][multiIndex[2]]}})</span>
            </view>
          </picker>
        </view>
      </view>
      
      
      
      
  
  
