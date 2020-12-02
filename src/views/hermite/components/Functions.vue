<template>
<div id="functions">
  <h2 class="title">Functions</h2>
  <div style="text-align: center;">
    <a-input class="search-input" v-model="search" placeholder="search function">
      <a-icon slot="prefix" type="search"/>
    </a-input>
  </div>

  <a-menu mode="inline" @click="handleClick">
    <a-menu-item key="Protein">
      <h3>
        <div class="icon-div">
          <img class="img1" src="@/assets/img/Protein_icon_Select.png">
          <img class="img2" src="@/assets/img/Protein Prepare_icon.png">
        </div>
        <span style="margin-left: 22px">Protein Prepare</span>
      </h3>
    </a-menu-item>
    <a-menu-item key="Ligand">
      <h3>
        <div class="icon-div">
          <img class="img1" src="@/assets/img/Ligand_icon_Select.png">
          <img class="img2" src="@/assets/img/Ligand Prepare_icon.png">
        </div>
        <span style="margin-left: 22px">Ligand Prepare</span>

      </h3>
    </a-menu-item>
    <a-menu-item key="Docking">
      <h3>
        <div class="icon-div">
          <img class="img1" src="@/assets/img/Docking_icon_Select.png">
          <img class="img2" src="@/assets/img/Docking_icon.png">
        </div>
        <span style="margin-left: 22px">Docking</span>
      </h3>

    </a-menu-item>
  </a-menu>
</div>
</template>

<script>
export default {
  name: 'Functions',
  data() {
    return {
      search: '',
    };
  },
  methods: {
    handleClick({ key }) {
      this.$emit('function-click', key);
    },
  },
};
</script>

<style scoped lang="scss">

#functions{
  padding-top: 10px;

  .title {
    //color: #fff;

  }

  .search-input{
    width: 90%;
    margin: 20px 0;
    //margin: 0 auto;
  }

  .ant-menu:not(.ant-menu-horizontal) .ant-menu-item-selected{
    background-color: #FAFAFA;

    h3{
      color: #14227A;
      .img2{
        display: none;
      }
    }

  }
  .ant-menu {
    border-top: 1px solid #EEEEEE;
    .ant-menu-item{
      height: 60px;
      line-height: 60px;
      border-bottom: 1px solid #EEEEEE;
      margin: 0;

      &::after{
        left: 0;
        right: auto;
        border-right: 3px solid #1F2676;
      }
      & h3:hover{
        color: #14227A;
      }

      &:hover .icon-div .img2{
        display: none;
      }

      .icon-div{
        position:relative;
        display: inline-block;
        vertical-align: text-top;
        .img1, .img2{
          position:absolute; z-index:0;
        }
        .img1{
          //margin-left: -22px;
        }

      }

    }
  }

}

</style>
