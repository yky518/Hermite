<template>
<div>
  <a-menu v-model="current" mode="horizontal"
          style="background-color: #ffffff;line-height: 42px;">
    <a-menu-item key="hermite">Hermite</a-menu-item>
    <a-menu-item key="fep">FEP</a-menu-item>
    <a-menu-item key="mhc">MHC</a-menu-item>
    <a-menu-item key="help">
      Help
    </a-menu-item>
    <a-menu-item key="about">
      About
    </a-menu-item>
    <a-menu-item key="contact">
      Contact
    </a-menu-item>
    <a-menu-item key="signup" style="float: right" @click="showRegister">
      <a-button class="signup-button">Sign Up</a-button>
    </a-menu-item>
    <a-menu-item key="login" style="float: right" @click="showLogin">
      Log In
    </a-menu-item>
    <a-menu-item style="float: right">
      <a-avatar src="https://zos.alipayobjects.com/rmsportal/ODTLcjxAfvqbxHnVXCYX.png"/>
      username
    </a-menu-item>

  </a-menu>

  <a-modal v-model="modalVisible" :footer="null" width="800px"
           :centered="true" :maskClosable="false">
    <a-row style="background-color: #1F2676;">
      <a-col  class="left-col" :span="12">
        Hermite
      </a-col>
      <a-col class="right-col" :span="12">
        <component :is="userComponent" @change-sign="changeSign"></component>
      </a-col>
    </a-row>
  </a-modal>
</div>
</template>

<script>
import Login from '@/components/user/Login.vue';
import Register from '@/components/user/Register.vue';
import Forget from '@/components/user/Forget.vue';

export default {
  name: 'Navbar',
  data() {
    return {
      showUser: false,
      current: ['mail'],
      modalVisible: false,
      userComponent: 'Login',
    };
  },
  methods: {
    success() {

    },
    showLogin() {
      this.modalVisible = true;
      this.userComponent = 'Login';
    },
    showRegister() {
      this.modalVisible = true;
      this.userComponent = 'Register';
    },
    changeSign(name) {
      console.log(name);
      this.userComponent = name;
    },
  },
  components: {
    Login,
    Register,
    Forget,
  },
};
</script>

<style scoped lang="scss">

.ant-menu{
  border: 0;

}

.ant-menu-horizontal > .ant-menu-item{
  border: 0;
}
.ant-menu-horizontal > .ant-menu-item-selected, .ant-menu-horizontal > .ant-menu-item:hover{
  color: #ffffff;
  border: 0;
  background-color: #3b4187;
}

/deep/ .ant-modal-body{
  padding: 0;
}

.left-col{
  width: 409px;
  color: white;
  padding: 20px 0 0 20px;
  font-size: 48px;
}

.right-col{
  width: 391px;
  padding: 50px 20px 0;
  text-align: center;
  background-color: #ffffff;
}

.signup-button{
  background-color: transparent;
  height: 40px;
  border-radius: 19px;
  border: 2px solid #FFFFFF;
  color: inherit;
}

.ignup-button:hover{
  color: #ffffff;
}

</style>
