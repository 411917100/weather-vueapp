<template>
  <div id="app">
    <div class="page-group">
      <div class="page">
          <v-header></v-header>
          <router-view/>
        <div>
          <!--<v-foot></v-foot>-->
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import Header from "./components/header.vue";
//  import Foot from "./components/foot.vue";
  export default {
    name: 'app',
    components:{
      "v-header":Header,
//      "v-foot":Foot,
    }
  }
</script>

<style>
  .page, .page-group{
    display: block;
    overflow:scroll;
    overflow-x:hidden;
  }
  .page{
    background-color: #ffffff;
  }
</style>
