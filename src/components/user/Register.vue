<template>
<div>
  <span class="title">注册</span>
  <a-form :form="form" class="modal-form">
    <a-form-item >
      <a-input placeholder="输入邮箱"
               v-decorator="['email',
              { rules: [{ required: true, message: 'Please input your note!' }] }]">
        <img class="icon-img" src="@/assets/img/email_icon@2x.png" alt="" slot="prefix">
      </a-input>
    </a-form-item>
    <a-form-item>
      <a-input class="email-input"
               v-decorator="[
          'code',
          { rules: [{ required: true, message: 'Please input your code' +
           '!' }] },
        ]"
               placeholder="输入验证码">
        <img class="icon-img" src="@/assets/img/Password_icon@2x.png" alt="" slot="prefix">
      </a-input>
      <a-button class="email-button">获得邮箱验证</a-button>
    </a-form-item>
    <a-form-item >
      <a-input placeholder="输入密码"
               v-decorator="['password',
              { rules: [{ required: true, message: 'Please input your password!' }] }]">
        <img class="icon-img" src="@/assets/img/email_icon@2x.png" alt="" slot="prefix">
      </a-input>
    </a-form-item>
    <a-form-item >
      <a-input placeholder="确认密码"
               v-decorator="['password2',
              { rules: [{ required: true, message: 'Please input your password2!' }] }]">
        <img class="icon-img" src="@/assets/img/Confirm_password_icon@2x.png" alt="" slot="prefix">
      </a-input>
    </a-form-item>
    <Verify @success="success" :show-button="false"
            :type="3" :bar-size="{width: '100%',height:'40px'}"></Verify>
    <a-form-item style="margin-top: 24px">
      <a-button class="submit-button" block html-type="submit">
        Submit
      </a-button>

      <span style="float: left">
              <a-radio></a-radio>
              同意
              <span style="color: #212982">用户协议</span>和
              <span style="color: #212982">隐私政策</span>
            </span>
      <span style="float: right">
              忘记密码
            </span>
    </a-form-item>
    <p class="bottom-text">已有账号，
      <span @click="$emit('change-sign', 'Login')">去登录</span>
    </p>
  </a-form>
</div>
</template>

<script>
import Verify from 'vue2-verify';

export default {
  name: 'Register',
  data() {
    return {
      form: this.$form.createForm(this, { name: 'coordinated' }),
    };
  },
  methods: {
    success() {

    },
  },
  components: {
    Verify,
  },
};
</script>

<style scoped lang="scss">

.title{
  font-size: 36px;
}

.modal-form{
  margin-top: 40px;

  /deep/ .ant-input-affix-wrapper{
    //width: 360px;
    .ant-input{

      height: 48px;
      background: #FAFAFA;
      border-radius: 30px;
      border: 1px solid #E8E8E8;
      &:not(:first-child) {
        padding-left: 40px;
      }

    }
  }

  .email-input{
    width: 210px;
  }
  .email-button {
    width: 140px;
    height: 48px;
    background: #FAFAFA;
    border-radius: 30px;
    border: 1px solid #E8E8E8;

  }

  .submit-button{
    height: 48px;
    background: #1F2676;
    border-radius: 30px;
    color: white;
  }

  .icon-img{
    height: 22px;
  }

  .bottom-text{
    margin-top: 40px;
    text-align: center;
    font-size: 16px;
    span{
      color: #1F2676;
      cursor: pointer;

    }
  }

  /deep/ .verify-bar-area{
    width: 360px;
    height: 48px;
    background: #FAFAFA;
    border-radius: 30px;
    border: 1px solid #E8E8E8;
    .verify-left-bar{
      border: 0;
      background-color: transparent;

      .verify-move-block{
        width: 48px;
        height: 48px;
        background: #FAFAFA;
        border-radius: 30px;
        border: 1px solid #E8E8E8;

      }
    }

  }
}
</style>
