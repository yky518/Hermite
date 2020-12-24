<template>
<div id="jobs">
<h2>
  <h3 class="title"><i>Jobs</i></h3>
  <a-table style="text-align: center"
    class="table"
    :pagination="false"
    :columns="columns"
    :data-source="data"
    rowKey="jobType"
  >
    <template slot="type" slot-scope="type">
      <img class="table-icon" v-if="type===1" src="@/assets/img/Protein_Prepare_icon@2x.png">
      <img class="table-icon" v-else-if="type===2" src="@/assets/img/Ligand_Prepare_icon@2x.png">
      <img class="table-icon" v-else src="@/assets/img/Docking_icon@2x.png">
    </template>
    <template slot="state" slot-scope="state">
      <div class="circle" v-if="state===0" style="background-color: #44C5AC"></div>
      <div class="circle" v-else-if="state===1" style="background-color: #F0C249"></div>
      <div class="circle" v-else style="background-color: #F06149"></div>
    </template>
    <template slot="operation">
      <img class="table-icon" src="@/assets/img/Kill_icon@2x.png">
      <img class="table-icon" src="@/assets/img/restarte_icon@2x.png">
      <img class="table-icon" src="@/assets/img/remove_icon@2x.png">
    </template>
  </a-table>
</h2>
</div>
</template>

<script>
const columns = [
  {
    title: 'Type',
    dataIndex: 'type',
    key: 'type',
    scopedSlots: { customRender: 'type' },
    width: 40,
  },
  {
    title: 'Name',
    dataIndex: 'name',
    key: 'name',
    width: 50,
  },
  {
    title: 'ID',
    dataIndex: 'id',
    key: 'id',
    width: 50,
  },
  {
    title: 'Time',
    dataIndex: 'time',
    key: 'time',
    width: 50,

  },
  {
    title: 'State',
    dataIndex: 'state',
    scopedSlots: { customRender: 'state' },
    align: 'center',
    key: 'state',
  },
  {
    title: 'Operation',
    dataIndex: 'operation',
    key: 'operation',
    scopedSlots: { customRender: 'operation' },
    width: 80,

  },
];

const data = [
  {
    type: 1,
    name: 'das',
    id: 'da324f',
    time: '23432',
    state: 0,
    operation: '',
  },
  {
    type: 2,
    name: 'das',
    id: 'da31sf',
    time: '23432',
    state: 1,
    operation: '',
  },
  {
    type: 3,
    name: 'das',
    id: 'd241sf',
    time: '23432',
    state: 2,
    operation: '',
  },
];

export default {
  name: 'Jobs',
  data() {
    return {
      data,
      pagination: {},
      loading: false,
      columns,
    };
  },
};
</script>

<style scoped lang="scss">
  #jobs{
    .title {
      //color: #fff;
      margin-left: 10px;
      color: gray;
    }
    .table-icon{
      height: 18px;
      margin: 0 2px;
    }
    .circle{
      height: 14px;
      width: 14px;
      border-radius: 50%;
      display: inline-block;
      vertical-align: middle;
    }

    /deep/ .ant-table tr > th{
      padding: 3px;
    }
    /deep/ .ant-table tr > td{
      padding: 3px;
    }

  }
</style>
