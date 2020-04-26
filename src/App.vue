<template>
  <div id="app"  >
                             
    <Poistenie />
    <div class="py-5 container bg-light">
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

#app{
  background-image: url("./assets/img/plaz.jpg");
  background-repeat: no-repeat;
  background-size: cover;
}

</style>
