<template>
  <div id="ligand">
    <h2>Ligand Prep</h2>
    <a-form :form="form" :label-col="{ span: 5 }" :wrapper-col="{ span: 12 }"
            class="form"
            @submit="handleSubmit">
      <div style="background: #FAFAFA;">

        <a-card>
          <span style="font-size: 12px">Job Name:</span><a-input class="jobname-input"></a-input>
        </a-card>
      </div>

      <a-collapse v-model="activeKey">
        <a-collapse-panel key="1" header="Load Ligands">
          <div style="margin: 10px 0 0 10px">
            <a-checkbox>Import Ligand File:</a-checkbox>
            <p style="text-align: right;margin-right: 10px">
              File: <a-input class="file-input"></a-input>
              <a-button class="file-button">
                Browse</a-button>
            </p>
            <a-checkbox>Load Database</a-checkbox>
            <a-checkbox-group v-model="databaseList"  style="text-align: left;margin-left: 20px">
              <a-row>
                <a-col :span="12" v-for="item in databaseOptions" :key="'database-'+item.label">
                  <a-checkbox :value="item.value">
                    {{item.label}}
                  </a-checkbox>
                </a-col>
              </a-row>
            </a-checkbox-group>
          </div>

        </a-collapse-panel>
        <a-collapse-panel key="2" header="Filter Molecules">
          <div style="margin: 15px">
            <a-radio-group v-model="filterList">
              <a-radio label="Custom">Custom</a-radio>
              <a-radio label="Set to ROS">Set to ROS</a-radio>
              <a-radio label="Set to RO3">Set to RO3</a-radio>
            </a-radio-group>
            <a-row gutter="5">
              <a-col :span="12">
                <h5>Atoms:</h5>
                <a-row>
                  <a-col :span="5">
                    <a-input class="slider-input" v-model="atoms[0]"></a-input>
                  </a-col>
                  <a-col :span="14">
                    <a-slider range :min="0" :max="500" v-model="atoms"/>
                  </a-col>
                  <a-col :span="5">
                    <a-input class="slider-input" v-model="atoms[1]"></a-input>
                  </a-col>
                </a-row>

              </a-col>
              <a-col :span="12">
                <h5>Rings:</h5>
                <a-row>
                  <a-col :span="5">
                    <a-input class="slider-input" v-model="rings[0]"></a-input>
                  </a-col>
                  <a-col :span="14">
                    <a-slider range :min="0" :max="80" v-model="rings"/>
                  </a-col>
                  <a-col :span="5">
                    <a-input class="slider-input" v-model="rings[1]"></a-input>
                  </a-col>
                </a-row>
              </a-col>
              <a-col :span="12">
                <h5>Molecular weight:</h5>
                <a-row>
                  <a-col :span="5">
                    <a-input class="slider-input" v-model="weight[0]"></a-input>
                  </a-col>
                  <a-col :span="14">
                    <a-slider range :min="0" :max="5000" v-model="weight"/>
                  </a-col>
                  <a-col :span="5">
                    <a-input class="slider-input" v-model="weight[1]"></a-input>
                  </a-col>
                </a-row>

              </a-col>
              <a-col :span="12">
                <h5>Rotatable bonds:</h5>
                <a-row>
                  <a-col :span="5">
                    <a-input class="slider-input" v-model="bonds[0]"></a-input>
                  </a-col>
                  <a-col :span="14">
                    <a-slider range :min="0" :max="200" v-model="bonds"/>
                  </a-col>
                  <a-col :span="5">
                    <a-input class="slider-input" v-model="bonds[1]"></a-input>
                  </a-col>
                </a-row>
              </a-col>
              <a-col :span="12">
                <h5>Hydrogen donors:</h5>
                <a-row>
                  <a-col :span="5">
                    <a-input class="slider-input" v-model="donors[0]"></a-input>
                  </a-col>
                  <a-col :span="14">
                    <a-slider range :min="0" :max="100" v-model="donors"/>
                  </a-col>
                  <a-col :span="5">
                    <a-input class="slider-input" v-model="donors[1]"></a-input>
                  </a-col>
                </a-row>
              </a-col>
              <a-col :span="12">
                <h5>LogP:</h5>
                <a-row>
                  <a-col :span="5">
                    <a-input class="slider-input" v-model="logP[0]"></a-input>
                  </a-col>
                  <a-col :span="14">
                    <a-slider range :min="-100" :max="100" v-model="logP"/>
                  </a-col>
                  <a-col :span="5">
                    <a-input class="slider-input" v-model="logP[1]"></a-input>
                  </a-col>
                </a-row>
              </a-col>
              <a-col :span="12">
                <h5>Hydrogen acceptors:</h5>
                <a-row>
                  <a-col :span="5">
                    <a-input class="slider-input" v-model="acceptors[0]"></a-input>
                  </a-col>
                  <a-col :span="14">
                    <a-slider range :min="0" :max="100" v-model="acceptors"/>
                  </a-col>
                  <a-col :span="5">
                    <a-input class="slider-input" v-model="acceptors[1]"></a-input>
                  </a-col>
                </a-row>
              </a-col>
            </a-row>
          </div>

        </a-collapse-panel>
        <a-collapse-panel key="3" header="Pronation state">
          <div style="margin: 15px">
            <p><a-radio>Retain origin state</a-radio></p>
            <p>
              <a-radio>Generate possible states, PH</a-radio>
              <a-input class="ligand-input"></a-input>
              +/-
              <a-input class="ligand-input"></a-input>
            </p>
          </div>

        </a-collapse-panel>
        <a-collapse-panel key="4" header="Generator Settings">
          <div style="margin: 15px">
            <p><a-radio>Generate tautomers</a-radio></p>
            <p>
              <a-radio>Generate conformations</a-radio>
              <a-input class="ligand-input"></a-input>
              for each
            </p>
<!--            <h4>Other Manipulate</h4>
            <p><a-radio>Flexible</a-radio></p>

            <a-form-item label="Output format" :wrapperCol="{span: 18}">
              <a-radio-group>
                <a-radio :value="1">
                  pdbqt
                </a-radio>
                <a-radio :value="2">
                  mol2
                </a-radio>
                <a-radio :value="3">
                  sdf
                </a-radio>
                <a-radio :value="4">
                  pdb
                </a-radio>
              </a-radio-group>
            </a-form-item>-->
          </div>

        </a-collapse-panel>

      </a-collapse>
    </a-form>
    <a-button block class="submit-button">Submit</a-button>

  </div>
</template>

<script>
const databaseOptions = [
  {
    label: 'Specs()',
    value: 'space',
  },
  {
    label: 'Maybridge()',
    value: 'maybridge',
  },
  {
    label: 'Vitas(774,117)',
    value: 'vitas',
  },
  {
    label: 'Enamine(?)',
    value: 'enamine',
  },
  {
    label: 'Bionet(?)',
    value: 'bionet',
  },
  {
    label: 'Chembridge(?)',
    value: 'chembridge',
  },
];
export default {
  name: 'Ligand',
  data() {
    return {
      activeKey: ['1'],
      form: {},
      databaseList: [],
      databaseOptions,
      atoms: [30, 400],
      rings: [30, 40],
      weight: [30, 400],
      bonds: [30, 100],
      donors: [30, 40],
      logP: [30, 40],
      acceptors: [30, 40],
      filterList: [],
    };
  },
  methods: {
    handleSubmit() {

    },
  },
};
</script>

<style scoped lang="scss">
  #ligand{
    height: 100%;
    position: relative;
    padding-bottom: 50px;
    .form{
      height: calc(100% - 50px);
      overflow: auto;
    }

    .slider-input{
      padding: 4px;
      text-align: center;
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

    .ligand-input{
      width: 54px;
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
  }
</style>
