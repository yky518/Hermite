<template>
<div >
  <a-input ref="searchInput" v-model="search" placeholder="输入关键词进行搜索">
    <a-icon slot="prefix" type="search" />
  </a-input>
  <div id="dialog">
    <a-row>
      <a-col :span="2">
        <a-avatar :size="32" icon="user" />
      </a-col>
      <a-col :span="22">
        <h4>DORR</h4>
        <p>Hey, please let me know how to get the LIGAND FRCMOD FILE</p>
        <a-row>
          <a-col :span="2">
            <a-avatar :size="32" icon="user" />
          </a-col>
          <a-col :span="22">
            <h4>DORR</h4>
            <p>Hey, please let me know how to get the LIGAND FRCMOD FILE</p>
          </a-col>
        </a-row>
      </a-col>
    </a-row>
    <a-row>
      <a-col :span="2">
        <a-avatar :size="32" icon="user" />
      </a-col>
      <a-col :span="22">
        <h4>DORR</h4>
        <p>Hey, please let me know how to get the LIGAND FRCMOD FILE</p>
        <a-row>
          <a-col :span="2">
            <a-avatar :size="32" icon="user" />
          </a-col>
          <a-col :span="22">
            <h4>DORR</h4>
            <p>Hey, please let me know how to get the LIGAND FRCMOD FILE</p>
          </a-col>
        </a-row>
      </a-col>
    </a-row>
    <a-row>
      <a-col :span="2">
        <a-avatar :size="32" icon="user" />
      </a-col>
      <a-col :span="22">
        <h4>DORR</h4>
        <p>Hey, please let me know how to get the LIGAND FRCMOD FILE</p>
        <a-row>
          <a-col :span="2">
            <a-avatar :size="32" icon="user" />
          </a-col>
          <a-col :span="22">
            <h4>DORR</h4>
            <p>Hey, please let me know how to get the LIGAND FRCMOD FILE</p>
          </a-col>
        </a-row>
      </a-col>
    </a-row>

  </div>

  <a-row>
    <a-col :span="20">
      <a-input placeholder="输入你的评论" class="dialog-input"></a-input>
    </a-col>
    <a-col :span="4">
      <a-button class="submit-button">发布</a-button>
    </a-col>
  </a-row>
</div>
</template>

<script>
export default {
  name: 'Dialog',
};
</script>

<style scoped lang="scss">
  #dialog{
    margin: 10px 0;

  }
  .dialog-input {
    height: 40px;
    background: #FAFAFA;
    border-radius: 30px;
    border: 1px solid #E8E8E8;
  }
  .submit-button{
    color: #ffffff;

    height: 40px;
    background: #1F2676;
    border-radius: 30px;
    margin-left: 10px;
  }
</style>
