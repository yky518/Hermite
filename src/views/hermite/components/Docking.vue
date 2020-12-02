<template>
<div id="docking">
  <a-form labelAlign="left">
    <div style="background: #FAFAFA;">
      <h2>Docking</h2>
      <a-card>
        <span>Job Name:</span><a-input class="jobname-input"></a-input>
      </a-card>
    </div>
    <a-collapse v-model="activeKey">
      <a-collapse-panel key="1" header="Load Protein">
        <div style="margin: 10px">
          <a-radio>Load <i>ProteinPrep</i> Result:</a-radio>
          <p style="text-align: right;margin-right: 10px">
            Job ID: <a-input class="file-input"></a-input>
            <a-button class="file-button">Load</a-button>
          </p>
          <a-radio>import <i>ProteinPrep</i> File:</a-radio>
          <p style="text-align: right;margin-right: 10px">
            File: <a-input class="file-input"></a-input>
            <a-button class="file-button">Browse</a-button>
          </p>
          <a-radio>Prepare a New Protein:</a-radio>
          <a-button block class="content-button">Protein Prep</a-button>
        </div>

      </a-collapse-panel>
      <a-collapse-panel key="2" header="Load Ligands">
        <div style="margin: 10px">
          <a-radio>Load <i>LigandPrep</i> Result:</a-radio>
          <p style="text-align: right;margin-right: 10px">
            Job ID: <a-input class="file-input"></a-input>
            <a-button class="file-button">Load</a-button>
          </p>
          <a-radio>import <i>LigandPrep</i> File:</a-radio>
          <p style="text-align: right;margin-right: 10px">
            File: <a-input class="file-input"></a-input>
            <a-button class="file-button">Browse</a-button>
          </p>
          <a-radio>Prepare a New Ligand:</a-radio>
          <a-button block class="content-button">Ligand Prep</a-button>
        </div>

      </a-collapse-panel>
      <a-collapse-panel key="3" header="Select Pocket">
        <div style="margin: 10px">
          <a-row style="text-align: center;border: 1px solid #333333;padding-top: 1rem">
            <a-col :span="8">
              <p>Center X Coord</p>
              <p>36.168</p>
            </a-col>
            <a-col :span="8">
              <p>Center Y Coord</p>
              <p>30.168</p>

            </a-col>
            <a-col :span="8">
              <p>Center Z Coord</p>
              <p>34.168</p>

            </a-col>
          </a-row>
          <h4>
            Select the box size: {{boxSize}} <a-icon type="question-circle" theme="filled"/>
          </h4>
          <a-slider :min="0" :max="500" v-model="boxSize"/>
          <div class="choose-title">Choose center of predicted binding site</div>
          <a-table :columns="bindingColumns" class="content-table"
                   rowKey="index" :row-selection="bindingRowSelection"
                   :data-source="bindingData" :pagination="false">
              <span slot="select" slot-scope="text" class="table-operation">
                <a-checkbox></a-checkbox>
              </span>
          </a-table>
          <div class="choose-title">Choose Center of Ligand</div>
          <a-table :columns="ligandColumns" class="content-table"
                   rowKey="index" :row-selection="ligandRowSelection"
                   :data-source="ligandData" :pagination="false">
              <span slot="select" slot-scope="text" class="table-operation">
                <a-checkbox></a-checkbox>
              </span>
          </a-table>
          <div class="choose-title">Choose Center of Selected Residues</div>
          <a-table :columns="residueColumns" class="content-table"
                   rowKey="index" :row-selection="residueRowSelection"
                   :data-source="residueData" :pagination="false">
              <span slot="select" slot-scope="text" class="table-operation">
                <a-checkbox></a-checkbox>
              </span>
          </a-table>
        </div>

      </a-collapse-panel>
      <a-collapse-panel key="4" header="Protein Flexibility">
        <div style="margin: 10px">
          <a-row class="flexibility-row">
            <a-col :span="8">
              <p>Residues</p>
              <p>SER127</p>
            </a-col>
            <a-col :span="8">
              <p>Chain</p>
              <p>A</p>

            </a-col>
            <a-col :span="8">
              <p>Select</p>
              <p>
                <a-radio></a-radio>
              </p>

            </a-col>
          </a-row>
          <a-row class="flexibility-row">
            <a-col :span="8">
              <p>Atom A</p>
              <p>SER127-C1</p>
            </a-col>
            <a-col :span="8">
              <p>Atom B</p>
              <p>SER127-N2</p>

            </a-col>
            <a-col :span="8">
              <p>Select</p>
              <p>
                <a-radio></a-radio>
              </p>

            </a-col>
          </a-row>
          <h5>Flexibility Chosen Helper</h5>
          <p>
            Sidechains within
            <a-input class="content-input"></a-input>
            Å of the center
            <a-button class="content-button">Load</a-button>
          </p>
          <p>
            Atoms within
            <a-input class="content-input"></a-input>
            Å of the center
            <a-button class="content-button">Load</a-button>
          </p>
          <p>
            All protein sidechains
            <a-button class="content-button">Load</a-button>
          </p>
          <p>
            Entire protein
            <a-button class="content-button">Load</a-button>
          </p>
        </div>

      </a-collapse-panel>
      <a-collapse-panel key="5" header="Docking Methods">
        <div style="margin: 10px">
          <a-radio>AutoDock Vina</a-radio>
          <div style="margin-left: 24px">
            <a-form-item label="Exhaustiveness" :labelCol="{span: 17}">
              <a-input class="method-input"></a-input>
            </a-form-item>
            <a-form-item label="Max num of binding modes" :labelCol="{span: 17}">
              <a-input class="method-input"></a-input>
            </a-form-item>
            <a-form-item label="Energy range" :labelCol="{span: 17}">
              <a-input class="method-input"></a-input>
            </a-form-item>
          </div>

          <a-radio>AutoDock 4</a-radio>
          <div style="margin-left: 24px">
            <a-form-item label="Num of GA runs" :labelCol="{span: 17}">
              <a-input class="method-input"></a-input>
            </a-form-item>
            <a-form-item label="Max num of evals" :labelCol="{span: 17}">
              <a-input class="method-input"></a-input>
            </a-form-item>
            <a-form-item label="Max num of generations" :labelCol="{span: 17}">
              <a-input class="method-input"></a-input>
            </a-form-item>
          </div>
          <a-radio>Use DeepDocking</a-radio>
          <div style="margin-left: 24px">
            <a-form-item label="Max num of docking" :labelCol="{span: 17}">
              <a-input class="method-input"></a-input>
            </a-form-item>
          </div>
        </div>

      </a-collapse-panel>
      <a-collapse-panel key="6" header="Results Processing">
        <div style="margin: 10px">
          <p>Kept best compounds</p>
          <a-row>
            <a-col :span="12">
              <a-radio></a-radio><a-input class="method-input"></a-input>%
            </a-col>
            <a-col :span="12">
              <a-radio></a-radio><a-input class="method-input"></a-input>#
            </a-col>
          </a-row>
          <a-radio>Calc ADMET for kept compounds</a-radio>
          <a-radio>Substructure analysis</a-radio>
        </div>

      </a-collapse-panel>
    </a-collapse>
    <a-button block class="submit-button">Submit</a-button>
  </a-form>
</div>
</template>

<script>
export default {
  name: 'Docking',
  data() {
    return {
      boxSize: 10.00,
      bindingColumns: [
        {
          title: 'pocket ID',
          dataIndex: 'id',
          key: 'id',
        },
        {
          title: 'relevance score',
          dataIndex: 'score',
          key: 'score',
        },
        {
          title: 'volume',
          dataIndex: 'volume',
          key: 'volume',
        },
        {
          title: 'druggability',
          dataIndex: 'ability',
          key: 'ability',
        },
      ],
      bindingData: [
        {
          id: 1,
          score: 100,
          volume: 600,
          ability: '20%',
        },
        {
          id: 2,
          score: 100,
          volume: 600,
          ability: '20%',
        },
      ],
      ligandColumns: [
        {
          title: 'compound',
          dataIndex: 'compound',
          key: 'compound',
        },
        {
          title: 'Chain',
          dataIndex: 'chain',
          key: 'chain',
        },
        {
          title: 'residue ID',
          dataIndex: 'residue',
          key: 'residue',
        },
        {
          title: 'Name',
          dataIndex: 'name',
          key: 'name',
        },
      ],
      ligandData: [
        {
          compound: 1,
          chain: 100,
          residue: 600,
          name: '20%',
        },
        {
          compound: 2,
          chain: 100,
          residue: 600,
          name: '20%',
        },
      ],
      residueColumns: [
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
      residueData: [
        {
          compound: 1,
          chain: 100,
          residue: 600,
          name: '20%',
        },
        {
          compound: 2,
          chain: 100,
          residue: 600,
          name: '20%',
        },
      ],
      activeKey: ['1'],
    };
  },
  computed: {
    bindingRowSelection() {
      return {
        onChange: (selectedRowKeys, selectedRows) => {
          console.log(`selectedRowKeys: ${selectedRowKeys}`, 'selectedRows: ', selectedRows);
        },
        getCheckboxProps: (record) => ({
          props: {
            disabled: record.name === 'Disabled User', // Column configuration not to be checked
            name: record.name,
          },
        }),
      };
    },
    ligandRowSelection() {
      return {
        onChange: (selectedRowKeys, selectedRows) => {
          console.log(`selectedRowKeys: ${selectedRowKeys}`, 'selectedRows: ', selectedRows);
        },
        getCheckboxProps: (record) => ({
          props: {
            disabled: record.name === 'Disabled User', // Column configuration not to be checked
            name: record.name,
          },
        }),
      };
    },
    residueRowSelection() {
      return {
        onChange: (selectedRowKeys, selectedRows) => {
          console.log(`selectedRowKeys: ${selectedRowKeys}`, 'selectedRows: ', selectedRows);
        },
        getCheckboxProps: (record) => ({
          props: {
            disabled: record.name === 'Disabled User', // Column configuration not to be checked
            name: record.name,
          },
        }),
      };
    },
  },
  created() {
    this.pocketData = [
      {
        id: 1,
        score: '100%',
        volume: 955,
        ability: 0.26,
      },
      {
        id: 2,
        score: '99%',
        volume: 345,
        ability: 0.67,
      },
      {
        id: 3,
        score: '54%',
        volume: 3523,
        ability: 0.16,
      },
      {
        id: 4,
        score: '65%',
        volume: 874,
        ability: 0.09,
      },
      {
        id: 5,
        score: '100%',
        volume: 955,
        ability: 0.26,
      },
    ];
  },
};
</script>

<style scoped lang="scss">
#docking {
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
  .content-input{
    width: 60px;
    height: 30px;
    background: #F7F7F7;
    border-radius: 20px;
    border: 1px solid #EBEBEB;
  }

  .method-input{
    width: 80px;
    height: 30px;
    background: #F7F7F7;
    border-radius: 20px;
    border: 1px solid #EBEBEB;
  }

  .file-button{
    margin-left: 5px;
    height: 30px;
    background: #1F2676;
    border-radius: 20px;
    color: #ffffff;
  }

  .content-button{
    margin-left: 5px;
    height: 30px;
    background: #1F2676;
    border-radius: 20px;
    color: #ffffff;
  }
  .choose-title{
    height: 30px;
    line-height: 30px;
    background: #F7F7F7;
    text-align: center;
    margin: 10px 0;
  }
  .flexibility-row{
    text-align: center;
    background: #F9F9F9;
    border-radius: 8px;
    padding: 0.5rem;
    margin: 10px 0;
  }

  .submit-button{
    height: 50px;
    background: #1F2676;
    color: #ffffff;

  }
}
</style>
