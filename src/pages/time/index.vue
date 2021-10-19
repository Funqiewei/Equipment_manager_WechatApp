<template>
<div>
  <van-toast id="van-toast"/>
        <div class="header">   
       </div>
            <picker mode="multiSelector" @change="bindMultiPickerChange"  :value="multiIndex" :range="newMultiArray">
              <div class="title">
                <span >&nbsp;&nbsp;点击选择时间：{{timestart}}</span>
              </div>
            </picker>
        
        <van-cell title-class="celltitle" title="选择下方时段"  />
        <div class="button1">
              <van-button 
                plain 
                size="normal"
                color="#3d7ef9"
                type="primary"
                block 
                @click="onClickButton1"
               >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8:00-12:00
               <image class='btnImg' src='/static/images/time.png'></image>
               </van-button>
               </div>
         <div class="button1">   
              <van-button 
                plain 
                size="normal"
                color="#3d7ef9"
                type="primary"
                block 
                @click="onClickButton2"
               >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;13:00-16:00
               <image class='btnImg' src='/static/images/time.png'></image>
               </van-button>
             </div>
             <div class="button1">
              <van-button 
                plain 
                size="normal"
                color="#3d7ef9"
                type="primary"
                block 
                @click="onClickButton3"
               >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;17:00-20:00
               <image class='btnImg' src='/static/images/time.png'></image>
               </van-button>
             </div>
             
              <div class="button1">
               <van-button 
                plain
                size="normal"
                color="#3d7ef9"
                type="primary"
                block 
                @click="onClickButton4"
               >&nbsp;&nbsp;现在就用
               <image class='btnImg' src='/static/images/use.png'></image>
               </van-button>
              </div>

              
           </div>   
</div>

</template>

<script>

import Toast from "vant-weapp/dist/toast/toast"
export default {
  data () {
    return {//日期
      date: true,
      show: false,
      buttonclick:false,
      timeSegment:'',
      timestart: "",
      TodayMonth:"",
      TodayDay:"",
      multiArray: [],
      multiIndex: [0,0],
      selectDay:"",
      selectMonth:"",
       updateTime:""
    }


  },
  computed: {
    newMultiArray: () => {
      var that=this
      let array = []; 
      const days = [];
      const months = []; 
      const nowDate = new Date();
      const date = {
          year: nowDate.getFullYear(),
          month: nowDate.getMonth() + 1,
          date: nowDate.getDate(),
      }
      const year=date.year
      const newmonth = date.month>10?date.month:'0'+date.month
      const day = date.date>10?date.date:'0'+date.date
      this.updateTime = date.year + '-' + newmonth + '-' + day
      that.TodayMonth=date.month
      that.TodayDay=day
      var maxday = new Date(year,that.TodayMonth,0); 
      console.log(that.TodayMonth,that.TodayDay,maxday.getDate())
      for (let i = that.TodayMonth; i <= that.TodayMonth; i++) {
        months.push("" + i);
      }
      array.push(months);
      
      for (let i = that.TodayDay; (i<=maxday.getDate())&&(i<=that.TodayDay+31); i++) {
        days.push("" + i);
      }
      
      array.push(days);
      return array;
    },
  },
  
  methods: {
     
    addDate(){
      var that =this
            const nowDate = new Date();
                  const date = {
                      year: nowDate.getFullYear(),
                      month: nowDate.getMonth() + 1,
                      date: nowDate.getDate(),
                  }
            const newmonth = date.month>10?date.month:'0'+date.month
            const day = date.date>10?date.date:'0'+date.date
            this.updateTime = date.year + '-' + newmonth + '-' + day
            that.TodayMonth=date.month
            that.TodayDay=day
            console.log(that.TodayMonth,that.TodayDay)
    },
//获取时间日期
          bindMultiPickerChange(e) {
          var that =this
          that.multiIndex = e.target.value;
          console.log("当前选择的时间", that.multiIndex);
          const index = that.multiIndex;
          const month = that.newMultiArray[0][index[0]];
          const day = that.newMultiArray[1][index[1]];
          that.selectDay=day
          that.selectMonth=month
          that.timestart =month+"月"+day+"号"
        },

        onClickButton1(){
        var that =this
          //console.log(event,"按钮被点击了")
          //that.client.publish('/mysmarthome/sub','按钮按下')
          //预约时间段
          if(that.selectDay==''){
              Toast.fail('未选择日期');
         }else{
           that.timeSegment='1'
            const url ="/pages/instrument/main?month="+that.selectMonth+"&day="+that.selectDay+"&timeSegment="+that.timeSegment
            wx.navigateTo({ url })
         }
         },

         onClickButton2(){
        var that =this
          //console.log(event,"按钮被点击了")
          //that.client.publish('/mysmarthome/sub','按钮按下')
          //预约时间段
          if(that.selectDay==''){
              Toast.fail('未选择日期');
         }else{
           that.timeSegment='2'
            const url ="/pages/instrument/main?month="+that.selectMonth+"&day="+that.selectDay+"&timeSegment="+that.timeSegment
            wx.navigateTo({ url })
         }
         },

         onClickButton3(){
        var that =this
          //console.log(event,"按钮被点击了")
          //that.client.publish('/mysmarthome/sub','按钮按下')
          //预约时间段
          if(that.selectDay==''){
              Toast.fail('未选择日期');
         }else{
           that.timeSegment='3'
           const url ="/pages/instrument/main?month="+that.selectMonth+"&day="+that.selectDay+"&timeSegment="+that.timeSegment
           wx.navigateTo({ url })
         }
         },

         onClickButton4(){
        var that =this
          //console.log(event,"按钮被点击了")
          //that.client.publish('/mysmarthome/sub','按钮按下')
          //预约时间段
            that.timeSegment='4'
            const url ="/pages/instrument/main?month="+that.selectMonth+"&day="+that.selectDay+"&timeSegment="+that.timeSegment
            wx.navigateTo({url})
         
         },
      },
         onShow() {
          var that = this;
          Toast.loading({
            message: "加载中...",
            forbidClick: true,
          });
        },
        // onLoad(){     
        //     Toast.loading({
        //     message: '加载中...',
        //     forbidClick: true,
        //       });
        //   },
}    


</script>


<style lang="scss" >
.button1{
  margin: 0 auto;
  width: 50%;
  left: 0px;
  right: 0px;
  margin-top:5px ;
  margin-bottom:20px;
}
.header{
  height: 5px;
  padding:25px 0px;
  background-color:#3d7ef9;
}
.btnImg {
  width: 50rpx;
  height: 50rpx;
  position: absolute;
  left: 30px;
  margin-top: 10px;
}
.title{
      left: 2px;
      font-size:25px;
      font-weight: 150;
      display:flex;
      justify-content: space-between;
      margin-top: 0px;
      margin-bottom: 10px;
      border-style:solid;
      color: #fff;
      border-top-color:#fff;
      background-color: #3d7ef9;
      border-color: #3d7ef9;
    }
.celltitle{
      left: 2px  !important;
      font-size:18px!important;
      font-weight: 150!important;
      display:flex!important;
      justify-content: space-between!important;
      margin-top: 10px!important;
      margin-bottom: 10px!important;
    }


</style>
