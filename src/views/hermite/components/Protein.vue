<template>
<div id="protein">
  <a-form :form="form" :label-col="{ span: 5 }" :wrapper-col="{ span: 12 }"
          @submit="handleSubmit">
    <div style="background: #FAFAFA;">
      <h2>Protein Prep</h2>
      <a-card>
        <span>Job Name:</span><a-input class="jobname-input"></a-input>
      </a-card>
    </div>
    <a-collapse v-model="activeKey">
      <a-collapse-panel key="1" header="Load Protein">
        <div style="margin: 10px 0 0 10px">
          <a-radio>Import PDB File:</a-radio>
          <p style="text-align: right;margin-right: 10px">
            File: <a-input class="file-input" v-model="pdbFile"></a-input>
            <a-upload :before-upload="loadFromPdb" :file-list="fileList">
              <a-button class="file-button">
                Browse
              </a-button>
            </a-upload>
          </p>
          <a-radio>PDB ID</a-radio>
          <p style="text-align: right;margin-right: 10px">File:
            <a-input class="file-input"></a-input><a-button class="file-button">
            Download</a-button></p>
        </div>

      </a-collapse-panel>
      <a-collapse-panel key="2" header="Model residues">
        <a-table :columns="residuesColumns" class="content-table"
                 rowKey="chain"
                 :data-source="residuesData" :pagination="false">
              <span slot="select" slot-scope="text" class="table-operation">
                <a-checkbox></a-checkbox>
              </span>
        </a-table>
      </a-collapse-panel>
      <a-collapse-panel key="3" header="Select Chain">
        <a-table :columns="chainColumns" class="content-table"
                 rowKey="index"
                 :data-source="chainData" :pagination="false">
              <span slot="select" slot-scope="text" class="table-operation">
                <a-checkbox></a-checkbox>
              </span>
        </a-table>
      </a-collapse-panel>
      <a-collapse-panel key="4" header="Other Manipulation">
        <div style="margin: 10px 0 0 10px">
          <p>
            <a-radio>Add missing side chains</a-radio>
          </p>
          <p>
            <a-radio>Add hydrogens</a-radio>
          </p>
          <p>
            <a-radio>Optimize the hydrogen binding network</a-radio>
          </p>
          <p>
            <a-radio>Protonation state, PH:</a-radio>
            <a-input class="ph-input"></a-input>
          </p>
        </div>

      </a-collapse-panel>

    </a-collapse>
    <a-button block class="submit-button">Submit</a-button>
  </a-form>
</div>
</template>

<script>
import globalBus from '@/eventBus/globalBus';

export default {
  name: 'Protein',
  data() {
    return {
      form: {},
      fileList: [],
      pdbFile: '',
      activeKey: ['1'],
      residuesColumns: [
        {
          title: 'Chain',
          dataIndex: 'chain',
          key: 'chain',
        },
        {
          title: 'Missing Residues',
          dataIndex: 'residues',
          key: 'residues',
        },
        {
          title: 'Select',
          key: 'select',
          scopedSlots: { customRender: 'select' },
        },
      ],
      residuesData: [
        {
          chain: 'fsadf',
          residues: 'dsaf',
        },
        {
          chain: 'fsawqerqwdf',
          residues: '234weg4',
        },
        {
          chain: 'dsfadf',
          residues: 'dsdsafasfaf',
        },
      ],
      chainColumns: [
        {
          title: 'Index',
          dataIndex: 'index',
          key: 'index',
        },
        {
          title: 'Type',
          dataIndex: 'type',
          key: 'type',
        },
        {
          title: 'Chain',
          dataIndex: 'chain',
          key: 'chain',
        },
        {
          title: 'First',
          dataIndex: 'first',
          key: 'first',
        },
        {
          title: 'Last',
          dataIndex: 'last',
          key: 'last',
        },
        {
          title: 'Select',
          key: 'select',
          scopedSlots: { customRender: 'select' },
        },
      ],
      chainData: [
        {
          index: '1',
          type: 'protein',
          chain: 'fsadf',
          first: '1',
          last: '100',
        },
        {
          index: '2',
          type: 'protein',
          chain: 'fsadf',
          first: '1',
          last: '100',
        },
        {
          index: '3',
          type: 'protein',
          chain: 'wrew',
          first: '1',
          last: '100',
        },
      ],
    };
  },
  methods: {
    handleSubmit() {

    },
    loadFromPdb(file) {
      console.log(file);
      this.fileList = [];
      this.pdbFile = file.name;
      // this.fileList.push(file);
      const pdbName = file.name.substring(0, file.name.lastIndexOf('.'));
      console.log(pdbName);
      globalBus.$emit('loadPdb', pdbName);

      return false;
    },
  },
};
</script>

<style scoped lang="scss">
 .jobname-input {
  width: 200px;
  margin-left: 10px;
  height: 30px;
  background: #F7F7F7;
  border-radius: 20px;
  border: 1px solid #EBEBEB;
}
 .file-input{
   width: 150px;
   height: 30px;
   background: #F7F7F7;
   border-radius: 20px;
   border: 1px solid #EBEBEB;
 }

 .ph-input{
   width: 100px;
   height: 30px;
   background: #F7F7F7;
   border-radius: 20px;
   border: 1px solid #EBEBEB;
 }

 .content-table{
   margin: 10px;
 }

 .file-button{
   margin-left: 5px;
   height: 30px;
   background: #1F2676;
   border-radius: 20px;
   color: #ffffff;
 }

 .submit-button{
   height: 50px;
   background: #1F2676;
   color: #ffffff;

 }

</style>
