<template>
  <div id="main">
    <Directory 
      @takeId="sendId"/>
    <List 
      :idOfDirectory="idOfDirectory"/>
  </div>
</template>

<script>
import Directory from "./components/Directory.vue";
import List from "./components/List.vue";

export default {
  name: "App",
  components: {
    Directory, List
  },
  data () {
    return {
      idOfDirectory: 0
    }
  },
  methods: {
    sendId: function(idOfDirectory) {
      this.idOfDirectory = idOfDirectory;
    }
  },
};
</script>

<style lang="scss">
  @import './assets/scss/mixing.scss';

  #main{
      display: flex;
      @include setContainers();
  }
</style>
