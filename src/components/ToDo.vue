<template>
  <div class="hello">
    <div class="holder">
<form @submit.prevent="addToArray(todo)">
  <input type="text" placeholder="Enter a task for the day" v-model="todo">
  <input type="checkbox" id="checkbox" v-model="checked">
</form>
  <button @click="clear()">Clear List</button>
<ul>
  <li v-for="(data, index) in todos" v-bind:key='index'>  
    {{ index + 1 }}. {{ data }}
  </li>

  

  <div v-bind:style="{ backgroundColor: bgColor, width: bgWidth, height: bgHeight }">
    {{ todo }}
  </div>

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
      checked: false,
      todo: '',
      todos: ["Beispiel ToDo"],
      bgColor: 'yellow',
      bgWidth: '100%',
      bgHeight: '100px'
    }
  }, 
  methods: {
    addToArray(todo) {
      this.todos.push(todo);
      this.todo = "";
      
      },
    clear() {
      this.todos = [];
    }
    },
  computed: {
    isEmpty: {
      get: function()
      {
        return this.todos.length - 1 >= 0;
      }
    },
      
      },
    }  
  
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

ul {
  list-style-type: none;
  padding: 0;
}
li {
  
  margin: 10px;
  text-align: left;
  margin-left: 40%;
  
}
#li1 {
  margin-bottom: 10px;
}
</style>
