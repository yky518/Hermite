<template>
<div id="results">
  <a-collapse accordion>
    <a-collapse-panel key="1" header="Results">
      <div style="text-align: center;margin:10px 0">
        <a-button class="content-button">2D Structure</a-button>
        <a-button class="content-button">Ligand Interaction</a-button>
      </div>

      <a-table :columns="columns" :data-source="data"
               :row-selection="rowSelection" rowKey="ligname">
      </a-table>
    </a-collapse-panel>
    <a-collapse-panel key="2" header="Help">
      <p>{ggsdgsdfg</p>
    </a-collapse-panel>
    <a-collapse-panel key="3" header="Used Params">
      <p>dasdfasfdasdf</p>
    </a-collapse-panel>
    <a-collapse-panel key="4" header="Explanation">
      <p>sdasfasdfadsf</p>
    </a-collapse-panel>
  </a-collapse>
</div>
</template>

<script>
export default {
  name: 'Results',
  data() {
    return {
      columns: [
        {
          title: 'Rank',
          key: 'rank',
          dataIndex: 'rank',
        },
        {
          title: 'Row',
          key: 'row',
          dataIndex: 'row',
        },
        {
          title: 'Ligname',
          key: 'ligname',
          dataIndex: 'ligname',
        },
        {
          title: 'Score',
          key: 'score',
          dataIndex: 'score',
        },
      ],
      data: [
        {
          rank: '1',
          row: '2',
          ligname: 'test',
          score: '100',
        },
      ],
    };
  },
  methods: {
  },
  computed: {
    rowSelection() {
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
};
</script>

<style scoped lang="scss">
.content-button{
  margin-left: 5px;
  height: 30px;
  background: #1F2676;
  border-radius: 20px;
  color: #ffffff;
}

</style>
