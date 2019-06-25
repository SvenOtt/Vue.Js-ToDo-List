<template>
  <div class="hello">
  <div class="holder">
    <form v-on:submit.prevent="addToArray(todo)">
      <input id="taskbox" type="text" placeholder="Enter a task for the day" v-model="todo" v-validate="'min:3'" name="todo">    
      <transition name="alert-in">

      <p class="alert" v-if="errors.has('todo')">{{errors.first('todo')}}</p>
      </transition>

   </form>
  
   <ul>
      <li v-on:mouseover="clickToEdit = false" v-on:mouseleave="clickToEdit = false"
       v-for="(todo, index) in todos" v-bind:key='index' v-bind:class="{ 'active': todo.active}" v-on:click="toggleActive(todo)" >
       {{ index + 1 }}. {{ todo }}

         <i  class = "fa fa-minus-circle" v-on:click="remove(index)">                    
        </i>

      <input id="edit" type="text" 
      v-show="clickToEdit" > 
        
      </li>

   <button @click="clear()">Clear List</button>
   

  <p v-if="isEmpty">You have things to do!</p>
  <p v-else>You have nothing to do.</p>

</ul>

</div>
  </div>
    
</template>


<script>

export default {
  name: 'ToDo',
  data() {
    return {
      selected: false, 
      clickToEdit: false,
      todo: '',
      todos: ["Finish this website", "Pizza Rotolo"],
      
      
    }
  }, 
  methods: {
    toggleActive: function(s){
            s.active = !s.active;
    },
    select(todo) {
      selected = true;
    },
    checkInd(indvar) {
      
    },
    
    addToArray(todo) {
      
        if (todo.length >= 3) {
          this.todos.push(todo);
          this.todo = "";
        } else {
          
          console.log('Not valid');
        
      }
      
    
      },
    clear() {
      this.todos = [];
    },
    remove(id) {
      this.todos.splice(id,1);
    
    }
    },
  computed: {
    isEmpty: {
      get: function()
      {
        return this.todos.length > 0;
      }
    },
      
      },
      checkout(){
        console.log(selected);
      }
    }  
  
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

@import "https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css";

.holder {
    background: #fff;
  }

  .alert {
    background: #fdf2ce;
    font-weight: bold;
    display: inline-block;
    padding: 5px;
    margin-top: -20px;
  }

  #taskbox {
    width: calc(100% - 40px);
    border: 0;
    padding: 20px;
    font-size: 1.3em;
    background-color: #323333;
    color: #687F7F;
  }
.holder {
  display: flex;
  justify-content: center;
  align-items: left;
  align-content: center;
  flex-direction: column;
  
}
  button {
    width: calc(60 - 40px);
    border: 0;
    padding: 20px;
    font-size: 1.3em;
    background-color: #d3e7e771;
    color: #687F7F;
    margin: auto;
    
  }
  ul {
    margin: 0;
    padding: 0;
    list-style-type: none;
  }
  
  ul li {
    padding: 20px;
    font-size: 1.3em;
    background-color: #E0EDF4;
    border-left: 5px solid #3EB3F6;
    margin-bottom: 2px;
    color: #3E5252;
  }

  #edit
  {
    margin: 0;
    padding: 0;
    font-size: 1.3em;
    background-color: #E0EDF4;
    margin-bottom: 2px;
    color: #3E5252;
  }

  p {
    text-align:center;
    padding: 30px 0;
    color: gray;
  }

  .container {
    box-shadow: 0px 0px 40px lightgray;
  }
  i{
    float: right;
  }

  .alert-in-enter-active {
    animation: bounce-in .5s

  }
  .alert-in-leave-active {
    animation: bounce-in .5s reverse;
  }
  form ul li.active{
    background-color:#8ec16d;
  }

  @keyframes bounce-in {
    0% {
      transform: scale(0);
    }
    50% {
      transform: scale(1.2);
    }
    100% {
      transform: scale(1);
    }
  }

</style>
