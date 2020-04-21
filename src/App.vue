<template>
  <div id="app" class="pb-5" :style="{'background-image': 'url(' + require('./assets/img/plaz.jpg') + ')' }" >
                             
    <Poistenie />
    <div class="pt-5 container bg-light">
      <Table></Table>
    </div>
    
  </div>
</template>

<script>

import Poistenie from "./components/Poistenie.vue";
import Table from "./components/Table.vue";

export default {
  name: "app",
  components: {
    Poistenie,
    Table,
  }
};
</script>

<style lang="scss">
@import 'node_modules/bootstrap/scss/bootstrap';
@import '../src/assets/sass/app.scss';


</style>
