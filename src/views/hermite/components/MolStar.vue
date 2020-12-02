<template>
<div id="test">

</div>
</template>

<script>
// import * as molstar from '@/assets/molstar';
import globalBus from '@/eventBus/globalBus';

export default {
  name: 'MolStar',
  props: ['pdb'],
  data() {
    return {
      viewer: null,

    };
  },
  created() {
    globalBus.$on('loadPdb', (pdb) => {
      this.viewer.loadPdb(pdb);
    });
  },
  mounted() {
    // eslint-disable-next-line no-undef
    const viewer = new molstar.Viewer('test', {
      layoutIsExpanded: false,
      layoutShowControls: false,
      layoutShowRemoteState: false,
      layoutShowSequence: true,
      layoutShowLog: false,
      layoutShowLeftPanel: true,

      viewportShowExpand: true,
      viewportShowSelectionMode: false,
      viewportShowAnimation: false,

      pdbProvider: 'rcsb',
      emdbProvider: 'rcsb',
    });

    this.viewer = viewer;
    // viewer.loadPdb('7bv2');
    // viewer.loadEmdb('EMD-30210', { detail: 6 });
  },
  methods: {
    loadPdb(pdb) {
      this.viewer.loadPdb(pdb);
    },
    loadUrl(url) {
      this.viewer.loadStructureFromUrl(url, '', '');
    },
  },
};
</script>

<style scoped>
@import "../../../assets/molstar.css";
#test{
  width: 100%;
  height: 100vh;
  position: relative;
  overflow: hidden;
}
</style>
