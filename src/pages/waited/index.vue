<template>

  <div>
      <van-tabs color="#3d7ef9"  :active="active" @change="onTabChange">
      <van-tab title="进行中">
              <van-card 
                title-class="cardtitle"
                :desc="time"
                title="已完成"
                thumb="/static/images/seat_abled.png"
              />

      </van-tab>

      <van-tab title="已完成">



      </van-tab>
    </van-tabs>
    </div>

</template>

<script>


export default {
  data () {
    return {
      active: 1,
      activeName: '1',
      name:"",
      useid:"2",
      time:"1"

    }


  },
  methods:{
      onTabChange(event) {
         // wx.showToast({
         //   title: `切换完成`,
         // });
        },
        
        onChange(event) {
            var that = this
            that.activeNames=event.mp.detail
        }
      
      },

  };


</script>

<style lang="scss" >

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
.cardtitle{
  position:absolute;
  color:#e60a0a;
  top: 10px;
  right:50px
}
</style>
