<template>
<div>
      <div>
           <swiper :indicator-dots="true" :autoplay="true":interval="5000" :duration="900" :circular="true"  >
                            <div v-for="(item,index) in imgUrls" :key="index">
                              <swiper-item>
                                <image :src="item" class="slide-image"/>
                              </swiper-item>
                            </div>
                          </swiper>               
      </div>      
      <div class="wrapper">
         <!--<div class="body-wrpper">
              <div class="body">
                  <div class="data-wrapper">
                          <div class="data">
                              <img class="data-logo" src="/static/images/tempture.png">
                              <div class="data-text">
                                  <div class="data-temp">温度</div>
                                  <div class="data-valUe">{{Temp}}℃</div>
                            </div>

                          </div>
                          <div class="data">
                              <img class="data-logo" src="/static/images/wet.png">
                              <div class="data-text">
                              <div class="data-temp">湿度</div>
                              <div class="data-valUe">{{Hum}}%</div>
                            </div>
                          </div>
                        </div>
                    </div>
                 </div>  
           <div class="body-wrpper">
              <div class="body">
                <div class="data-wrapper">
                        <div class="data">
                            <img class="data-logo" src="/static/images/light.png">
                            <div class="data-text">
                                <div class="data-temp">光照</div>
                                <div class="data-valUe">{{Light}}lx</div>
                          </div>
                        </div>

                        <div class="data">
                            <img class="data-logo" src="/static/images/beep.png">
                            <div class="data-text">
                                <div class="data-temp">指示灯1</div>
                                <div class="data-valUe">
                                  <switch @change="onLedChange" :checked="Led" color="#3d7ef9"/>
                                </div>
                          </div>
                        </div>
                      </div>
                   </div>
                 </div> 
                 
           <div class="body-wrpper">
              <div class="body">
                <div class="data-wrapper">
                        <div class="data">
                            <img class="data-logo" src="/static/images/LED.png">
                            <div class="data-text">
                                <div class="data-temp">蜂鸣器</div>
                                <div class="data-valUe">
                                  <switch @change="onBeepChange" :checked="Beep" color="#3d7ef9"/>
                                </div>
                          </div>
                        </div>
                      </div>
                   </div>
                 </div>   -->


              
            <div class="button1">
              <van-button 
                plain 
                size="large"
                color="#3d7ef9"
                type="primary"
                @click="onClickButton"
               >&nbsp;&nbsp;&nbsp;&nbsp;使用指南
               <image class='btnImg' src='/static/images/guide.png'></image>
               </van-button>
               </div>

             <div class="button2">
              <van-button 
                plain 
                size="large"
                color="#3d7ef9"
                type="primary"
                @click="onClickButton2"
               >&nbsp;&nbsp;&nbsp;&nbsp;项目开发介绍
               <image class='btnImg' src='/static/images/guide.png'></image>
               </van-button>
               </div>
               
              <div class="button3">
              <van-button 
                plain 
                size="large"
                color="#3d7ef9"
                type="primary"
                @click="onClickButton3"
               >&nbsp;&nbsp;&nbsp;&nbsp;项目开发介绍
               <image class='btnImg' src='/static/images/guide.png'></image>
               </van-button>
               </div>
            <div class="bottom-wrapper">
                      <div class="bottom-title">
                            <span>{{City}}-{{Area}}&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>
                            <span>空气质量:{{AirValue}}-{{AirQualiy}}</span>                      
                  </div>
                    <div class="bottom-text">
                            <span>{{Weather}}</span>
                            <span>{{Tempreal}}℃</span>   
                          </div>
                          <div class="weather-advice">&nbsp;&nbsp;&nbsp;&nbsp;{{WeatherAdvice}}</div>
                 </div>
            </div>
            <van-toast id="van-toast"/>
  </div>           
</template>


<script>
import Toast from "vant-weapp/dist/toast/toast"
import { connect } from "mqtt/dist/mqtt.js";
const mqttUrl = 'wxs://mqtt.emqttedu.xyz:8084/mqtt'
const token= '1'

export default {
  name:"SimpleSwiper",
    props: {
        images: {
          type: Array
      }
  },
  data () {
    return{
        client:{},
        AirValue:0,
        AirQualiy:'请求中',
        Beep:false,
        Tempreal:0,
        Temp:0,
        Hum:0,
        Light:0,
        Led:false,
        City:'绍兴市',
        Area:'上虞区',
        Weather:'请求中',
        WeatherAdvice:'请求中',
        imgUrls: [
          '/static/images/swiper1.png',
          '/static/images/swiper2.png'
          ]

    };
  },

  components: {},

  methods: {
    onLedChange(event){
      var that = this
      console.log(event.mp.detail.value)
      let sw= event.mp.detail.value
      that.Led =sw
     if(sw){
       that.client.publish('/mysmarthome/sub','{"LED_SW":1}',function (err) {
       if(!err){
         console.log("成功发送命令-开灯")
       }
     })
     }else{
      that.client.publish('/mysmarthome/sub','{"LED_SW":0}',function (err) {
       if(!err){
         console.log("成功发送命令-关灯")
       }
     })
     };
    },
      onClickButton(){
      const url ="/pages/guide/main"
      wx.navigateTo({ url })
      },
      onClickButton2(){
      wx.request({
          url: 'http://106.15.57.106:8080/equipment_server/device1/link', //仅为示例，并非真实的接口地址
          data:{
            code:"5",
            time:"222"},
          header: {'Content-Type':'application/x-www-form-urlencoded' // 默认值
          },
          method:'post',
          success (res) {
            console.log(res)
            console.log('this is post request result' + res.data)
          },
          fail(res)
          {
            console.log("失败")
          }
        })
      },
      
      
    onBeepChange(event){
      var that = this
      console.log(event)
      let sw= event.mp.detail.value
      that.Beep = sw
      if(sw){
        that.client.publish('/mysmarthome/sub','{"Beep":1}',function (err) {
        if(!err){
          console.log("成功发送命令-开蜂鸣器")
        }
      })
     }else{
      that.client.publish('/mysmarthome/sub','{"Beep":0}',function (err) {
       if(!err){
         console.log("成功发送命令-关蜂鸣器")
       }
     })
     };
    }
  },

  created () {
 let app = getApp()
  },

 onLoad(){
   var that = this
   that.client = connect(mqttUrl)
    Toast.loading({
    message: '加载中...',
    forbidClick: true,
      });
      
   wx.login({
      success (res) {
        if (res.code) {
          //发起网络请求
          wx.request({
            url: 'wxs://mqtt.emqttedu.xyz:8084/mqtt/mysmarthome/sub',
            data: {
              code: res.code
            }
          },
          console.log('登录成功！')
          )
        //console.log(res.code)
        //that.client.publish('/mysmarthome/sub',res.code)发res.code
        } else {
          console.log('登录失败！' + res.errMsg)
        }
      }
    })

   
   that.client.on('connect',function(){
     console.log("成功连接mqtt")
     that.client.subscribe("/mysmarthome/pub",function(err){
       if(!err){
            console.log("成功订阅设备上行topic")
       }
     })

     that.client.on('message',function(topic,message){
      let dataFromDev = {}
      dataFromDev =JSON.parse(message)//字节流转换
      console.log(dataFromDev)
      that.Temp = dataFromDev.Temp
      that.Hum = dataFromDev.Hum
      that.Light = dataFromDev.Light
      that.Beep = dataFromDev.Beep
      console.log(topic)
      
     })
   }) 

    

        wx.getLocation({
        type: 'wgs84',// 默认为wgs84的gps坐标，如果要返回直接给openLocation用的火星坐标，可传入'gcj02'
        success (res) {
        const latitude = res.latitude
        const longitude = res.longitude
        const key =	'6e8d686b843f4c2ea3b0b5e0bbc7d95b' 
        wx.request({//天气
        url: `https://devapi.qweather.com/v7/weather/now?location=${longitude},${latitude}&key=${key}`, //和风天气api地址
        success (res) {
         //console.log(res.data)
          const{now}=res.data
          //console.log(now)
          that.Humreal=now.humidity
          that.Tempreal=now.temp
          that.Weather=now.text
        }
      })

        wx.request({//生活建议
        url: `https://devapi.qweather.com/v7/indices/1d?type=0&location=${longitude},${latitude}&key=${key}`, //和风天气api地址
        success (res) {
          //console.log(res.data)
          const{daily}=res.data
          //console.log(daily)
          that.WeatherAdvice=daily[8].text
        }
      })

        wx.request({//空气质量
        url: `https://devapi.qweather.com/v7/air/now?location=${longitude},${latitude}&key=${key}`, //和风天气api地址
        success (res) {
          //console.log(res)
          const{now,station}=res.data
          that.AirQualiy=now.category
          that.AirValue=now.aqi
        }
      })
    }
  })
    
 }
};
</script>
<style lang="scss"scoped>
.slide-image {
    width: 100%;
    height: 100%;
    
  }
.btnImg {
  width: 50rpx;
  height: 50rpx;
  position: absolute;
  left: 30px;
  margin-top: 10px;
}
.button1{
  position:fixed;
  left:0px;
  right:0px;
  margin: 0 auto;
  width: 50%;
}
.button2{
  position:fixed;
  left:0px;
  right:0px;
  margin: 0 auto;
  width: 50%;
  margin-top: 60px;
}
.wrapper{
  padding:15px;
  .bottom-wrapper{ 
    background-color:#3d7ef9 ;
    border-radius: 20px;
    color: #fff;
    box-shadow: #d6d6d6 0px 0px 5px;
    padding: 15px 30px;
    position: fixed;
    bottom: 0;
    right:15px;
    left:15px;
    overflow:hidden;
    margin-top:5px;
    
    .bottom-title{
      display: flex;
      
    }
    .bottom-text{
      font-size:32px;
      font-weight: 150;
      display:flex;
      justify-content: space-between;
    }
    .weather-advice{
      margin-top:10px;
      font-size: 12px;
      justify-content: space-between;
      display:flex;
    }
    
  }

  .data-wrapper{
      margin-top: 0px;
      display: flex;
      justify-content: space-between;
      margin-bottom: 10px;
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
}
</style>
