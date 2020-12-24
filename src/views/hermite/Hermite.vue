<template>
<div>
  <a-layout class="layout">
    <a-layout-header style="padding: 0;height: 42px" class="top">
      <Navbar class="nav"></Navbar>
    </a-layout-header>
    <a-layout-content style="padding: 0;margin-top: 42px;">
      <a-layout>
        <a-layout-sider collapsible v-model="leftCollapsed" collapsedWidth="0" width="350"
                        class="left-sider" :trigger="null"
                        :zeroWidthTriggerStyle="{backgroundColor: '#fff',color: '#333333'}">
          <Functions @function-click="functionClick"></Functions>
          <Jobs></Jobs>
        </a-layout-sider>
        <a-layout-content :style="{position: 'relative',height: '100vh',}">

          <div :style="{marginLeft: leftCollapsed?'0px': '350px',
          marginRight: rightCollapsed?'0px': '400px',
          textAlign: 'center',position: 'absolute',right: '0', left: '0' }">
<!--            <a-button>Surface View</a-button>
            <a-button>Surface View</a-button>
            <a-button>Surface View</a-button>-->
            <VueDragResize style="z-index: 1;right: 0;left: auto;cursor: pointer"
                           :isResizable="false" :w="28" :h="28"
                           @clicked="rightCollapsed = !rightCollapsed"
                           :parentLimitation="true" axis="y">
              <div class="fold-right">

                <div>
                  <a-icon type="menu-fold" style="font-size: 20px"></a-icon>
                </div>
                <!--                <a-icon type="down" />-->
              </div>
            </VueDragResize>
            <VueDragResize style="z-index: 1;cursor: pointer;" :isResizable="false" :w="28" :h="28"
                           :parentLimitation="true" axis="y"
                           @clicked="leftCollapsed = !leftCollapsed">
              <div class="fold-left">
                <div>
                  <a-icon type="menu-fold" style="font-size: 20px"></a-icon>
                </div>
                <!--                <a-icon type="down" />-->
              </div>
            </VueDragResize>

            <MolStar ref="molstar"></MolStar>
          </div>

        </a-layout-content>
        <a-layout-sider collapsible :reverseArrow="true" v-model="rightCollapsed"
                        collapsedWidth="0" width="400"
                        class="right-sider"
                        :zeroWidthTriggerStyle="{backgroundColor: '#fff',color: '#333333'}">
            <component :is="inputComponent"></component>
        </a-layout-sider>
      </a-layout>
    </a-layout-content>

  </a-layout>

  <div id="chat" @click="isChatVisible = true" style="cursor: pointer">
    <img class="icon-img" src="@/assets/img/chat_icon@2x.png">
  </div>

  <a-modal title="全部" v-model="isChatVisible" :footer="null">
    <Dialog></Dialog>
  </a-modal>
</div>
</template>

<script>
import Navbar from '@/components/Navbar.vue';
import Functions from '@/views/hermite/components/Functions.vue';
import Ligand from '@/views/hermite/components/Ligand.vue';
import Jobs from '@/views/hermite/components/Jobs.vue';
import Protein from '@/views/hermite/components/Protein.vue';
import Docking from '@/views/hermite/components/Docking.vue';
import MolStar from '@/views/hermite/components/MolStar.vue';
import VueDragResize from 'vue-drag-resize';
import Results from '@/views/hermite/components/Results.vue';
import Dialog from '@/views/hermite/components/Dialog.vue';

export default {
  name: 'Hermite',
  data() {
    return {
      search: '',
      leftCollapsed: false,
      rightCollapsed: false,
      rightVisible: false,
      placement: 'left',
      inputComponent: '',
      isChatVisible: false,
      pdbFile: '',
      pdbUrl: '',
      fileList: [],

    };
  },
  created() {
    this.inputComponent = 'Results';
  },
  methods: {
    onClose() {
      this.visible = false;
    },
    onChange(e) {
      this.placement = e.target.value;
    },
    functionClick(key) {
      this.inputComponent = key;
      this.rightCollapsed = false;
    },
    loadPdb() {
      console.log(this.pdbFile);
      this.$refs.molstar.loadPdb(this.pdbFile);
    },
    loadUrl() {
      console.log(this.pdbUrl);
      this.$refs.molstar.loadUrl(this.pdbUrl);
    },
    loadFromPdb(file) {
      console.log(file);
      this.fileList = [];
      this.fileList.push(file);
      const pdbName = file.name.substring(0, file.name.lastIndexOf('.'));
      console.log(pdbName);
      this.$refs.molstar.loadPdb(pdbName);

      return false;
    },
  },
  components: {
    Navbar,
    Functions,
    Ligand,
    Jobs,
    Protein,
    Docking,
    MolStar,
    VueDragResize,
    Results,
    Dialog,
  },
};
</script>

<style scoped lang="scss">

.icon-img{
  height: 22px;
}

.top {
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 100;
}
.nav{
  position: relative;
  z-index: 10;
}

.left-sider {
  height: calc(100vh - 42px);
  position: fixed;
  left: 0;
  top: 42px;
  background-color: #fff;
  overflow: auto;
  z-index: 100;
  .files-button{
    background-color: #1F2676;
    color: white;
    height: 50px;
  }

}

.right-sider{
  background-color: white;
  height: calc(100vh - 42px);
  position: fixed;
  right: 0;
  top: 42px;
  bottom: 0;
  overflow: hidden;

  /deep/ .ant-collapse-content > .ant-collapse-content-box{
    padding: 0;
  }

}

.fold-left{
  margin: 5px 0;
  //padding: 3px;
  background-color: white;
  border: 1px solid gray;
  border-radius: 3px;
}
.fold-right{
  margin: 5px 0;
  //padding: 3px;
  background-color: white;
  border: 1px solid gray;
  border-radius: 3px
}
.layout{
  .left-arrow, .right-arrow {
    //position: ;
    //left: 0;
    //top: 0;
    //height: 100vh;
    width: 20px;

    &:hover {
      background-color: cadetblue;
    }

    .icon {
      margin-top: 50vh;
    }
  }
  .left-arrow{
    float: left;
  }
  .right-arrow{
    float: right;
  }
  .left-panel{
    width: 200px;
    background-color: #2c3e50;
  }
  .view-panel{
    background-color: burlywood;
    width: auto;
  }
  .right-panel{
    //height: 100vh;
    background-color: antiquewhite;
  }
}

#chat {
  position: fixed;
  bottom: 10vh;
  right: 0;
  background-color: #1F2676;
  padding: 10px;
  border-radius: 20px 0 0 20px/20px 0 0 20px;
}

</style>

<style>
.vdr.active::before{
  outline:none;
}
</style>
