<template>
  <div>
     <div class="header">
      <div v-if="isLogin">
         <div class="header-title">请登录</div>
          <div class="header-info">Please Login Your Account</div>
      </div>
      <div v-else>
         <div class="header-title">请注册</div>
          <div class="header-info">Please Register Your Account</div>
      </div>    
     </div>

     <div class="body">
          <div class="login-form">
               <van-field 
               label="用户名"
               placeholder="请输入用户名"
                :value="inputUserName"
                @change="onUserNameChange"
               />
               <van-field 
               label="密码"
               type="password"
               placeholder="请输入密码"
                :value="inputPassword"
                @change="onPasswordChange"
               />
                
                <div v-if="!isLogin">
                   <van-field 
                    label="注册手机号"
                    placeholder="请输入手机号"
                    :value="inputContact"
                    @change="onContactChange"
                    />
                </div>

          </div>

          <van-button 
          type="primary"
          slot="button"
          round block color="#3d7ef9"
          border="true"
          @click="onClick" 
          >
          {{isLogin?"登录":"注册"}}
          </van-button>
          
          <div class="other-option">
            <div @click="onOptionClick"> 
              <span >{{isLogin?"注册账号":"登陆账户"}}</span></div>  
                <span style="margin:0 30px">|</span>

            <div @click="onForgetClick"> 
              <span password="true">忘记密码</span></div> 
          </div>
          
          <div class="coppyright-wrapper">
            <span class="copyright">©Power By Zuoge</span>
          </div>

        <van-dialog
            use-slot
            title="找回密码"
            :show="showFindPassword"
            show-cancel-button
            @confirm="onFindPassWordConfirm"
            @cancel="onFindPassWordCancel"
            transistion="fade"
            >

        <van-field 
            label="手机号"
            title-width="60px"
            placeholder="请输入绑定手机号"
            :value="inputContact"
            @change="onContactChange"
            transistion="fade"
            disable-default-padding="true"
         />

        </van-dialog>
        <van-dialog
                use-slot
                title="重置密码"
                :show="showReSetPassword"
                show-cancel-button
                @confirm="onReSetWordConfirm"
                transistion="fade"
                >
             <van-field 
                label="用户名"
                title-width="60px"
                :value="inputUserName"
                readonly
               />
               <van-field 
                label="新密码"
                type="password"
                title-width="60px"
                placeholder="请输入新密码"
                :value="inputPassword"
                @change="onPasswordChange"
                @cancel="onPasswordCancel"
               />
          </van-dialog>
          <van-toast id="van-toast" />

     </div>
  </div>
</template>;

<script>
import Toast from "vant-weapp/dist/toast/toast"
export default {
  data () {
    return {
      inputUserName:"",
      inputPassword:"",
      inputContact:"",
      isLogin:true,
      showFindPassword:false,
      showReSetPassword:false
    }


  },
  methods:{
    onUserNameChange(event){
      var that=this 
      //"pages/login/main",
      that.$set(that,"inputUserName",event.mp.detail)
      console.log("当前用户名：",event.mp.detail)
    },

    onPasswordChange(event){
      var that=this  
      that.$set(that,"inputPassword",event.mp.detail)
       console.log("当前密码：",event.mp.detail)
    },

    onContactChange(event){
          var that=this  
          that.$set(that,"inputContact",event.mp.detail)
          console.log("请输入手机号：",event.mp.detail)
        },

    onClick(event){
          var that=this  
          Toast.loading({
            duration:0,//持续展示轻提示
            forbidClick:true,//禁止提示时被点击
            massage:that.isLogin?"登陆中...":"注册中..."
          })
          //console.log(event.mp.detail)

          setTimeout(()=>{
            if(!that.isLogin){
              wx.setStorage({
              key:"user",
              data:{
                Username:that.inputUserName,
                Password:that.inputPassword,
                Contact:that.inputContact
              },
              success (res) {
                console.log(res);
                console.log("注册成功！")
                Toast.success("注册成功")
                that.isLogin=true
        
                },
              fail (res) {
                console.log(res)
                console.log("注册失败！")
                Toast.fail("注册失败")

              }
            });
          }else{
            wx.getStorage({
            key: 'user',
            success (res){
                //console.log(res.data)
                if(that.inputUserName === res.data.Username && that.inputPassword === res.data.Password)
                {
                  Toast.success("登陆成功")
                  setTimeout(()=>{wx.switchTab({
                    url: "/pages/index/main"
                  });},500)
                }else{
                  Toast.fail("用户名/密码错误")
                  }
              },
              fail (res) {
                console.log(res)
                Toast.fail("数据库暂无注册用户")
              }
            })
          }},1000)
        },

        onOptionClick(event){
            var that=this  
            that.isLogin=!that.isLogin
            console.log(`切换注册/登录被点击了,当前处于${that.isLogin?"登录":"注册"}状态！`)
        },

        onForgetClick(event){
            var that=this  
            that.showFindPassword=!that.showFindPassword
        },

        onFindPassWordConfirm(event)
        {   
          var that=this  
           wx.getStorage({
            key: 'user',
            success (res){
                //console.log(res.data)
                if(that.inputContact === res.data.Contact)
                {
                  that.showReSetPassword=false
                  that.inputUserName=res.data.inputUserName
                  that.showReSetPassword=true
                  console.log("找到该用户信息",res.data.Contact)
                }else{
                  Toast.fail("无该用户信息")
                  that.inputContact=""
                }
              },
              fail (res) {
                //console.log(res)
                Toast.fail("数据库暂无注册用户")
                that.inputContact=""
              }
            })
            that.showFindPassword=!that.showFindPassword
        },
        onReSetWordConfirm(event){
          var that = this
          wx.setStorage({
              key:"user",
              data:{
                Username:that.inputUserName,
                Password:that.inputPassword,
                Contact:that.inputContact
              },
              success (res) {
                console.log(res);
                console.log("重置成功！")
                Toast.success("重置成功")
                },

              fail (res) {
                console.log(res)
                console.log("重置失败！")
                Toast.success("重置失败")
              }
            })
        },
        onFindPassWordCancel(event){
        var that = this
        that.inputUserName=""
        that.inputPassword=""
        that.inputContact=""
        },
        onReSetWordCancel(event){
        var that = this
        that.inputUserName=""
        that.inputPassword=""
        that.inputContact=""
        }
  }
    
};


</script>

<style lang="scss"scoped>

.header{
  height: 50px;
  padding:25px 0px;
  background-color:#3d7ef9;
  
  
  .header-title{
    font-size:28px;
    margin-top: -10px;
    font-weight: 500;
    color:#fff;
    margin-left: 20px;
  }

  .header-info{
    font-size:14px;
    color:#fff;
    margin-left: 20px;
  }

}

.body{

    border-radius: 15px 15px 0 0;
    background-color: #fff;
    padding: 20px;
    .login-form{
      margin-bottom: 30px;
    }

    .other-option{
      display: flex;
      justify-content: center;
      margin-top:20px;
      color: #9f9f9f;
    }

    .coppyright-wrapper{
      display: flex;
      font-size:14px;
      justify-content: center;
      .copyright{
        color: #bbb9b9;
        position: fixed;
        bottom: 50px;
      }
    }

}


</style>
