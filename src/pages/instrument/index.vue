<template>
 
<div>
          <div class="header">
            <div class="seatStatusList">
                <img class="statusLabel" src="/static/images/seat_abled.png">
                <span>可选用</span>
                <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
                <img class="statusLabel" src="/static/images/slected_seat.png">
                <span>已选中</span>
                <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
                <img class="statusLabel" src="/static/images/seat_used.png">
                <span>不可选</span>
                <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
              </div>
          </div>


      <div>

        <div class="chooseseatStatusList"  >
              <img class="statusLabel"  @click="onClickseat($event,'0')"  v-if="Seatflag[0]=='0'" src="/static/images/seat_abled.png">
              <img class="statusLabel"    v-else-if="Seatflag[0]=='2'" src="/static/images/seat_used.png">
              <img  class="statusLabel" @click="onClickseat($event,'0')" v-else src="/static/images/slected_seat.png"  >


              <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
              <img class="statusLabel"  @click="onClickseat($event,'1')"  v-if="Seatflag[1]=='0'" src="/static/images/seat_abled.png">
              <img class="statusLabel"    v-else-if="Seatflag[1]=='2'" src="/static/images/seat_used.png">
               <img  class="statusLabel" @click="onClickseat($event,'1')" v-else src="/static/images/slected_seat.png"  >

              <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
              <img class="statusLabel"  @click="onClickseat($event,'2')" v-if="Seatflag[2]=='0'" src="/static/images/seat_abled.png">
              <img class="statusLabel"    v-else-if="Seatflag[2]=='2'" src="/static/images/seat_used.png">
               <img  class="statusLabel" @click="onClickseat($event,'2')" v-else src="/static/images/slected_seat.png"  >
              <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>

            </div>
              <div class="chooseseatStatusList"  >
              <img class="statusLabel"  @click="onClickseat($event,'3')"  v-if="Seatflag[3]=='0'" src="/static/images/seat_abled.png">
              <img class="statusLabel"    v-else-if="Seatflag[3]=='2'" src="/static/images/seat_used.png">
              <img  class="statusLabel" @click="onClickseat($event,'3')" v-else src="/static/images/slected_seat.png"  >


              <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
              <img class="statusLabel"  @click="onClickseat($event,'4')"  v-if="Seatflag[4]=='0'" src="/static/images/seat_abled.png">
              <img class="statusLabel"    v-else-if="Seatflag[4]=='2'" src="/static/images/seat_used.png">
               <img  class="statusLabel" @click="onClickseat($event,'4')" v-else src="/static/images/slected_seat.png"  >

              <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
              <img class="statusLabel"  @click="onClickseat($event,'5')" v-if="Seatflag[5]=='0'" src="/static/images/seat_abled.png">
              <img class="statusLabel"    v-else-if="Seatflag[5]=='2'" src="/static/images/seat_used.png">
               <img  class="statusLabel" @click="onClickseat($event,'5')" v-else src="/static/images/slected_seat.png"  >
              <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>

            </div>
            
            </div>
                  <div class="chooseseatStatusList"  >
                  <img class="statusLabel"  @click="onClickseat($event,'6')"  v-if="Seatflag[6]=='0'" src="/static/images/seat_abled.png">
                  <img class="statusLabel"    v-else-if="Seatflag[6]=='2'" src="/static/images/seat_used.png">
                  <img  class="statusLabel" @click="onClickseat($event,'3')" v-else src="/static/images/slected_seat.png"  >


                  <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
                  <img class="statusLabel"  @click="onClickseat($event,'7')"  v-if="Seatflag[7]=='0'" src="/static/images/seat_abled.png">
                  <img class="statusLabel"    v-else-if="Seatflag[7]=='2'" src="/static/images/seat_used.png">
                  <img  class="statusLabel" @click="onClickseat($event,'4')" v-else src="/static/images/slected_seat.png"  >

                  <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
                  <img class="statusLabel"  @click="onClickseat($event,'8')" v-if="Seatflag[8]=='0'" src="/static/images/seat_abled.png">
                  <img class="statusLabel"    v-else-if="Seatflag[8]=='2'" src="/static/images/seat_used.png">
                  <img  class="statusLabel" @click="onClickseat($event,'5')" v-else src="/static/images/slected_seat.png"  >
                  <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
          </div>  
          
              <view class="page-body">
                <view class="button-sp-area">
                  <button type="primary" plain="true">预约选中座位</button>
                </view>
              </view>
      </div> 
                
         
</div>
</template>

<script>
export default {
  data () {
    return {
      Seatflag:['0','0','0','0','2','2','2','2','2'],
      showAppoint:[false,false,false,false,false,false,false,false,false],
      id:'0'
    }


  },
  methods:{
    onClickseat:function(event,id){
            var that=this  
            for (let index = 0; index < that.Seatflag.length; index++) {
            const element = that.Seatflag[index];
                  if(that.Seatflag[index]!='2'){
                    that.$set(that.Seatflag,index,'0')
                }
            }
           
            if(that.Seatflag[id]=='1'){
                that.$set(that.Seatflag,id,'0')
            }else if(that.Seatflag[id]=='0'){
                that.$set(that.Seatflag,id,'1')
            }
            that.$set(that.showAppoint,id,true)

            console.log("被点击了",that.Seatflag,that.showAppoint,id)
            that.$set(that.showAppoint,id,false)
        },

  }
    
};


</script>

<style lang="scss"scoped>

.seatStatusList {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100px;
}
.chooseseatStatusList {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100px;
  margin-top: 10px;
  margin-left: 10px;
}
.statusLabel{
  margin-top: 36px;
  margin-bottom: 36px;
  width:50px;
  height:50px;
  
}
.page {
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  color: #999;
}
.header {
  background-color:#fff ;
  border-radius: 0px 0px 5px 5px;
  display: flex;
  justify-content: space-around;
  padding: 0 8px;
  box-shadow: #d6d6d6 0px 0px 5px;
  height: 100px;
  overflow: hidden;
  background-color: #fff;
}
.main {
  background-color: #eee;
  flex-grow: 1;
  overflow: hidden;
}
.footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 1.2rem;
  background-color: #fff;
}
.mrgR60 {
  margin-right: 0.6rem;
}
button{
  margin-top: 30rpx;
  margin-bottom: 30rpx;
}
.button-sp-area{
  margin: 0 auto;
  width: 60%;
}
.mini-btn{
  margin-right: 10rpx;
}
.data-wrapper{
      margin-top: 20px;
      display: flex;
      justify-content: space-between;
      .data{
        background-color: #fff;
        width: 150px;
        height:80px;
        border-radius: 20px;
        display: flex;
        justify-content: space-around;
        padding: 0 8px;
        box-shadow: #d6d6d6 0px 0px 5px;
        .data-logo{
          height: 36px;
          width: 36px;
          margin-top: 15px;
        }
        .data-text{
           margin-top: 15px;
           columns: #7f7f7f; ;
           .data-title{
             text-align:middle;
           }
           .data-value{
             font-size: 26px;
           }
        }
      }
  }



</style>
