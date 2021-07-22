<template>
  <li @click="$emit('focus', itemOfDirectory.id-1)">
    <img 
      class="logo" 
      v-bind:src="require('../assets/' + itemOfDirectory.logo)" />
      {{ itemOfDirectory.name }}
  </li>
</template>

<script>
export default ({
  props: {
    itemOfDirectory: {
      type: Object,
      required: true
    }
  }
})
</script>

<style lang="scss">
  @import '../new_todo/src/assets/scss/variables.scss';
  @import '../new_todo/src/assets/scss/mixing.scss';

  li {
    background-color: $templateForDirectory;
    display: flex;
    min-height: 24px;
    font-size: 15px;
    cursor: pointer;
    padding: 5px 20px 5px 5px;
    border-radius: 3px;
    margin-bottom: 5px;
    opacity: 1;
}

li:hover {
    opacity: 0.5;
    transition: all 0.2s ease-in-out;
}
 
.logo {
    padding-right: 15px;
    @include setSizeForImages();
}
</style>
