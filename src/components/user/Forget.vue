<template>
  <div>
    <span class="title">忘记密码</span>
    <a-form :form="form" class="modal-form">
      <a-form-item >
        <a-input placeholder="输入邮箱"
                 v-decorator="['email',
              { rules: [{ required: true, message: 'Please input your note!' }] }]">
          <img src="@/assets/img/email_icon.png" alt="" slot="prefix">
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
          <img src="@/assets/img/Password_icon.png" alt="" slot="prefix">
        </a-input>
        <a-button class="email-button">获得邮箱验证</a-button>
      </a-form-item>
      <a-form-item >
        <a-input placeholder="输入密码"
                 v-decorator="['email',
              { rules: [{ required: true, message: 'Please input your note!' }] }]">
          <img src="@/assets/img/email_icon.png" alt="" slot="prefix">
        </a-input>
      </a-form-item>
      <a-form-item >
        <a-input placeholder="通过邮箱"
                 v-decorator="['email',
              { rules: [{ required: true, message: 'Please input your note!' }] }]">
          <img src="@/assets/img/email_icon.png" alt="" slot="prefix">
        </a-input>
      </a-form-item>
      <a-form-item>
        <Verify @success="success" @error="alert('error')" :show-button="false"
                :type="3" :bar-size="{width: '100%',height:'40px'}"></Verify>
      </a-form-item>
      <a-form-item>
        <a-button class="submit-button" block html-type="submit">
          确定
        </a-button>

        <span style="float: left">
              <a-radio></a-radio>
              同意
              <span style="color: #212982">用户协议</span>和
              <span style="color: #212982">隐私政策</span>
            </span>
      </a-form-item>
    </a-form>
  </div>
</template>

<script>
import Verify from 'vue2-verify';

export default {
  name: 'Forget',
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
  margin-top: 58px;

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
