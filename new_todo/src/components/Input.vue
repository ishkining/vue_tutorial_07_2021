<template>
  <div
    id="itemForAdding">
    <input 
      id="text" 
      type="text" 
      placeholder="Type new Action:" 
      @input="$emit('input', $event.target.value)"
      />
      
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: String
    }
  }
}
</script>

<style lang="scss">
  @import '../new_todo/src/assets/scss/variables.scss';
  @import '../new_todo/src/assets/scss/mixing.scss';

  #text {
    width: 200px;
    height: 30px;
    color: #0f550f;
    font-family: 'Open Sans', sans-serif;
    font-size: 15px;
    background-color: #f1f6fb;
  }

  #itemForAdding {
    background : $templateForAdding;

    input {
      width: 200px;
      height: 30px;
      color: #0f550f;
      font-family: 'Open Sans', sans-serif;
      font-size: 15px;
      background-color: #f1f6fb;
    }

    input::placeholder {
      color : blue;
    }

    img {
      opacity: 0.6;
    }

    img:hover {
      opacity: 1;
      transition: all 0.2s ease-in-out;
    }
  } 

</style>