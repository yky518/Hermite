<template>
<div>
<h2>
  <h2 class="title">Jobs</h2>
  <a-table
    :columns="columns"
    :data-source="data"
    rowKey="jobType"
  >
    <template slot="action" slot-scope="text">Delete</template>
  </a-table>
</h2>
</div>
</template>

<script>
const columns = [
  {
    title: 'JobType',
    dataIndex: 'jobType',
    key: 'jobType',
  },
  {
    title: 'JobID',
    dataIndex: 'jobID',
    key: 'jobID',
  },
  {
    title: 'JobState',
    dataIndex: 'jobState',
    key: 'jobState',
  },
];

const data = [
  {
    jobType: '23432',
    jobID: 'da3241sf',
    jobState: 0,
  },
  {
    jobType: '3424',
    jobID: '3241',
    jobState: 0,
  },
  {
    jobType: '1234',
    jobID: 'da3412sf',
    jobState: 0,
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
.title {
  //color: #fff;
}
</style>
