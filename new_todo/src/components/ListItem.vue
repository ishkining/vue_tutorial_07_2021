<template>
  <li v-if="typeOfInput === 'checkbox'">
    <img 
      :id="itemOfList.order" 
      class="moveAction" 
      v-bind:src="require('../assets/dots.png')" 
      @mousedown="$emit('beginMovingItem', itemOfList.action)" 
      @mouseleave ="$emit('moveItem', itemOfList.order, itemOfList)" >
    <Checkbox 
      :itemOfList="itemOfList"/>
    <img 
      class="removeAction" 
      v-bind:src="require('../assets/remove.png')"
      @click="$emit('removeAction', itemOfList.order)">
  </li>

  <li v-else-if="typeOfInput === 'text'">
    <img 
      id="addAction" 
      v-bind:src="require('../assets/add.png')" 
      v-on:click="addNewAction()" 
      @click="$emit('addNewAction', newAction)">
    <Input 
      :itemOfList="itemOfList"
      :newAction="newAction" 
      v-model="newAction"/>
  </li>
</template>

<script>
import Input from './Input.vue'
import Checkbox from './Checkbox.vue'

export default {
  components: {
    Input, Checkbox
  },
  props: {
    itemOfList: {
      type: Object,
      required: false
    },
    typeOfInput: {
      type: String,
      required: false
    }
  },
  data ()  {
    return {
      newAction: ''
    }
  },
  watch: {
    newAction() {
      console.log(this.newAction)
    }
  }
}
</script>

<style lang="scss">
  @import '../new_todo/src/assets/scss/variables.scss';
  @import '../new_todo/src/assets/scss/mixing.scss';


  li {
    background: #2596be;
    padding-inline-start: 20px;
  }

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

  .moveAction {
    @include setSizeForImages();
    cursor: grab;
  }

  .removeAction {
    @include setSizeForImages();
    float: right;
    margin-left: auto;
    cursor: pointer;
  }

  #addAction {
    @include setSizeForImages();
    margin-right: 10px;
  }
</style>