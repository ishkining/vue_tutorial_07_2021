<template>
  <div id="input">
    <div>
      <input 
        class="checkbox" 
        type="checkbox" 
        :id="itemOfList.action" 
        :name="itemOfList.action" 
        v-model="itemOfList.done">
    </div>
    <label :for="itemOfList.action">{{itemOfList.action}}</label>
  </div>
</template>

<script>
export default {
  props: {
    itemOfList: {
      type: Object,
      required: false
    }
  }
}
</script>

<style lang="scss">
  @import '../new_todo/src/assets/scss/variables.scss';
  @import '../new_todo/src/assets/scss/mixing.scss';

  .checkbox {
    @include setSizeForImages();
  } 
  
  label {
    margin-left: 10px;
    display:  block;
    text-align: center;
    align-self: center;
    font-size: 15px;
    white-space: nowrap;
    text-overflow: clip;
  }

  #input {
    width: 250px;
    display: flex;
  }
</style>