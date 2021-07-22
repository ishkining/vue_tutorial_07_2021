<template>
  <div id="list">
    <h1>Start:</h1>
    <ul>
      <ListItem 
        v-for="item in unDoneActions" 
        :key="item.id"
        :itemOfList="item"
        typeOfInput="checkbox"
        @removeAction="deleteThisAction" 
        @beginMovingItem="beginMovingItem"
        @moveItem="moveItem"/>
      <ListItem 
        :itemOfList="item"
        typeOfInput="text"
        @addNewAction="addNewAction"/>
    </ul>
    <h1>Done:</h1>
      <ListItem 
        v-for="item in doneActions" 
        :key="item.id"
        :itemOfList="item"
        typeOfInput="checkbox" />
    <ul>

    </ul>
  </div>
</template>

<script>
import ListItem from './ListItem.vue'

export default {
  components: {
    ListItem
  },
  props:{
    idOfDirectory: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      listOfActions: [
        [{
            action : "Learn Vue",
            done: false,
            order: 1
        },
        {
            action : "Make to do list",
            done: false,
            order: 2
        },
        {
            action : "Play Chess",
            done: false,
            order: 3
        }],
        [{
            action : "Read a book",
            done: false,
            order: 1
        },
        {
            action : "Talk with Nico",
            done: false,
            order: 2
        }],
        [{
            action : "Fuck myself",
            done: false,
            order: 1
        },
        {
            action : "Die",
            done: false,
            order: 2
        }]],
      movingObject: false
    }
    
  },
  computed: {
    unDoneActions: function () {
      console.log(this.listOfActions[this.idOfDirectory].filter(object => object.done === false));
      return this.listOfActions[this.idOfDirectory].filter(object => object.done === false)
    },
    doneActions: function () {
      return this.listOfActions[this.idOfDirectory].filter(object => object.done === true)
    }
  },
  methods: {
    addNewAction: function(nameOfNewAction) {
      this.listOfActions[this.idOfDirectory].push({
        action: nameOfNewAction,
        done: false,
        order: this.listOfActions[this.idOfDirectory].length + 1
      });
    },
    deleteThisAction: function(orderOfItem) {
      this.listOfActions[this.idOfDirectory].forEach(element => {
        if(element.order > orderOfItem) {
            element.order -= 1;
        }
      });
      this.listOfActions[this.idOfDirectory].splice(this.listOfActions[this.idOfDirectory].findIndex(object => object.order === orderOfItem), 1);
    },
    beginMovingItem: function() {
      this.movingObject = true;
    }
    ,moveItem: function(oldOrder, item) {
      if(this.movingObject)
      {
        let newOrder = Math.round((window.event.pageY - 85) / 36) + 1;
        if(oldOrder < newOrder){
          newOrder -= 1;
        }
        this.listOfActions[this.idOfDirectory].forEach(element => {
          if(oldOrder > newOrder) {
            if(element.order >= newOrder && element.order <= oldOrder) {
              element.order += 1;
            }
          }
          if(oldOrder < newOrder) {
            if(element.order <= newOrder && element.order >= oldOrder) {
              element.order -= 1;
            }
          }
        });
        item.order = newOrder;
        this.listOfActions[this.idOfDirectory].sort((a, b) => { return a.order - b.order });
        this.movingObject = false;
      }
    }
  },
}
</script>

<style lang="scss">
@import '../new_todo/src/assets/scss/variables.scss';
@import '../new_todo/src/assets/scss/mixing.scss';

  #list {
      width: 80%;
      background: #e9f5f9;
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