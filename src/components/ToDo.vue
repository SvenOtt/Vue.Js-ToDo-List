<template>
  <div class="hello">
    <div class="holder">
      <form v-on:submit.prevent="addToArray(todo)">
        <input
          id="taskbox"
          type="text"
          placeholder="Enter a task for the day"
          v-model="todo"
          v-validate="'min:3'"
          name="todo"
        >
        <transition enter-active-class="animated flipInX" leave-active-class="animated flipOutX">
          <p class="alert" v-if="errors.has('todo')">{{errors.first('todo')}}</p>
        </transition>
      </form>

      <ul>
        <transition-group name="list" enter-active-class="animated bounceInUp" leave-active-class="animated bounceOutDown">
        <li v-for="(task, index) in todos" v-bind:key="index" style="position:relative;">
          <label v-on:click="toggleActive(task)">{{ index + 1 }}. {{ task.name }}</label>

          <i class="fa fa-minus-circle" v-on:click="remove(index)"></i>
          <form
            v-on:submit.prevent="toggleInactive(task)"
            style="position:absolute; top:0.5em; left:0.5em;"
          >
            <input id="edit" type="text" v-show="task.clickToEdit" v-model="task.name">
          </form>
        </li>
</transition-group>
        <button @click="clear()">Clear List</button>

        <p v-if="isEmpty">You have things to do!</p>
        <p v-else>You have nothing to do.</p>
        
      </ul>

    </div>
  </div>
</template>


<script>
export default {
  name: "ToDo",
  data() {
    return {
      selected: false,
      todo: "",
      globaleClick: false,

      todos: [
        {
          name: "Finish this website",
          clickToEdit: false
        },
        {
          name: "Pizza Rotolo",
          clickToEdit: false
        }
      ]
    };
  },
  methods: {
    toggleActive(task) {
      console.log("click registers");
      task.clickToEdit = true;
    },

    toggleInactive(task) {
      console.log("submit registers");
      task.clickToEdit = false;
    },

    addToArray(todo) {
      if (todo.length >= 3) {
        let newTodo = {
          name: todo,
          clickToEdit: false
        };
        this.todos.push(newTodo);
        this.todo = "";
      } else {
        console.log("Not valid");
      }
    },
    clear() {
      this.todos = [];
    },
    remove(id) {
      this.todos.splice(id, 1);
    }
  },
  computed: {
    /*isActive: {
      toggleActive(todos) {
            event.target.active = !event.target.active;
            if (event.target.active === true){
              console.log ('is active');
            }
            else if (event.target.active === false){
              console.log ('is inactive')
            }
            
            else {
              console.log ('is undefined');
            }
    },
      

    },*/

    isEmpty: {
      get: function() {
        return this.todos.length > 0;
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css";
@import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1";

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
  color: #687f7f;
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
  color: #687f7f;
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
  background-color: #e0edf4;
  border-left: 5px solid #3eb3f6;
  margin-bottom: 2px;
  color: #3e5252;
}

#edit {
  margin: 0;
  padding: 0;
  font-family: "Montserrat";
  font-size: 1.3em;
  background-color: #e0edf4;
  margin-bottom: 2px;
  color: #3e5252;
  border-style: solid;
  border-color: lightgray;
}

p {
  text-align: center;
  padding: 30px 0;
  color: gray;
}

.container {
  box-shadow: 0px 0px 40px lightgray;
}
i {
  float: right;
}
</style>
