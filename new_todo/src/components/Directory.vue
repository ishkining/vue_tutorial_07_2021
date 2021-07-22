<template>
  <div id="directory">
    <ul>
      <DirectoryItem 
        v-for="item in listOfDirectory" 
        :key="item.id"
        :itemOfDirectory="item"
        @focus="saveFocus"/>
    </ul>
  </div>
</template>

<script>
import DirectoryItem from './DirectoryItem.vue'

export default {
  components: {
    DirectoryItem
  },
  data() {
    return {
      listOfDirectory: []
    }
  },
  async created() {
    const request = await fetch('https://api.jsonbin.io/b/60efe4290cd33f7437c8bfee/2', {
      method: 'GET',
      headers: {
        'secret-key': '$2b$10$W1MJsd9OXC4g30FQhga4FuZqYEDFaY8QrsUrkfLUCL0tblCMYsOVq'
      }
    });

    const data = await request.json();
    this.listOfDirectory = data.data;
    console.log(this.listOfDirectory);
  },
  methods: {
    saveFocus: function(idOfDirectory) {
      this.$emit('takeId', idOfDirectory)
    }
  },
}
</script>


<style lang="scss">
  @import '../new_todo/src/assets/scss/variables.scss';
  @import '../new_todo/src/assets/scss/mixing.scss';

  #directory{
    width: 20%;
    background: $templateForDirectory;
    border: 1px solid #92cbdf;
    @include setContainers();
  }

  ul {
    display: block;
    list-style-type: none;
    margin-block-start: 1em;
    margin-block-end: 1em;
    margin-inline-start: 0px;
    margin-inline-end: 0px;
    padding-inline-start: 40px;
    align-items: center;
}
</style>