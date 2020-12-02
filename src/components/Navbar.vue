<template>
<div>
  <a-menu v-model="current" mode="horizontal"
          style="background-color: #1f2676;line-height: 62px;color: white">
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
      Sign Up
    </a-menu-item>
    <a-menu-item key="login" style="float: right" @click="showLogin">
      Log In
    </a-menu-item>

  </a-menu>

  <a-modal v-model="modalVisible" :footer="null" width="1000px">
    <a-row>
      <a-col  class="left-col" :span="12">
        Hermite
      </a-col>
      <a-col class="right-col" :span="12">
        <component :is="userComponent" @forget="userComponent = 'Forget'"></component>
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
  background-color: #1F2676;
  width: 508px;
  height: 650px;
  color: white;
  padding: 20px 0 0 20px;
  font-size: 48px;
}

.right-col{
  width: 491px;
  padding: 100px 70px 0;
  text-align: center;

}

</style>
