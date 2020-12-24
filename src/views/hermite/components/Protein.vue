<template>
<div id="protein">
  <h2>Protein Prep</h2>
  <a-form class="form"
    :form="form" :label-col="{ span: 5 }" :wrapper-col="{ span: 12 }"
    @submit="handleSubmit">
    <div style="background: #FAFAFA;">
      <a-card>
        <span style="font-size: 12px">Job Name:</span><a-input class="jobname-input"></a-input>
      </a-card>
    </div>
    <a-collapse v-model="activeKey">
      <a-collapse-panel key="1" header="Load Protein">
        <div style="margin: 15px">
          <a-radio>Import PDB File:</a-radio>
          <p style="text-align: right;margin-right: 10px">
            File: <a-input classfile-in="put" v-model="pdbFile"></a-input>
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
                 size="small"
                 :row-selection="{ selectedRowKeys: selectedResidues, onChange: onSelectResidues }"
                 rowKey="chain"
                 :data-source="residuesData" :pagination="false">
              <span slot="confirm" slot-scope="text" class="table-operation">
                <a-checkbox></a-checkbox>
              </span>
        </a-table>
      </a-collapse-panel>
      <a-collapse-panel key="3" header="Select Chain">
        <a-table :columns="chainColumns" class="content-table"
                 size="small"
                 :row-selection="{ selectedRowKeys: selectedChain, onChange: onSelectChain }"
                 rowKey="index"
                 :data-source="chainData" :pagination="false">
              <span slot="select" slot-scope="text" class="table-operation">
                <a-checkbox></a-checkbox>
              </span>
        </a-table>
      </a-collapse-panel>
      <a-collapse-panel key="4" header="Other Manipulation">
        <div style="margin: 15px">
          <p>
            <a-checkbox>
              Add missing side chains
            </a-checkbox>
          </p>
          <p>
            <a-checkbox>
              Add hydrogens
            </a-checkbox>
          </p>
          <p>
            <a-checkbox>
              Optimize the hydrogen binding network
            </a-checkbox>
          </p>
          <p>
            <a-checkbox>
              Protonation state, PH:
            </a-checkbox>
            <a-input class="ph-input"></a-input>
          </p>
        </div>

      </a-collapse-panel>

    </a-collapse>
  </a-form>

  <a-button block class="submit-button">Submit</a-button>
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
      selectedResidues: [],
      selectedChain: [],
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
          title: 'Confirm',
          key: 'confirm',
          scopedSlots: { customRender: 'confirm' },
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
    onSelectResidues(selectedRowKeys) {
      console.log('selectedRowKeys changed: ', selectedRowKeys);
      this.selectedResidues = selectedRowKeys;
    },
    onSelectChain(selectedRowKeys) {
      console.log('selectedRowKeys changed: ', selectedRowKeys);
      this.selectedChain = selectedRowKeys;
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
  #protein{
    height: 100%;
    position: relative;
    padding-bottom: 50px;
    .form{
      height: calc(100% - 50px);
      overflow: auto;
    }
  }
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
   position: absolute;
   bottom: 0;

 }

</style>
