<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <h3>You have {{ todosCount }} todos</h3>
    <div>
      <input
        v-model="newTodoName"
        @keyup.enter="addTodo"
        placeholder="Add a TODO" 
        type="text" />
    </div>
    <div>
      <ul>
        <li v-for="(todo, index) in todos" :key="todo.id">
          <span>{{ todo.name }}</span>
          <button @click="deleteTodo(index)">X</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  data() {
    return {
      newTodoName: '',
      todos: [
        {
          id: 1,
          name: 'One',
        },
        {
          id: 2,
          name: 'Two',
        },
        {
          id: 3,
          name: 'Three',
        },
      ],
      swearWords: ['fart', 'butt hair', 'minion']
    };
  },
  computed: {
    todosCount(){
      return this.todos.length
    }
  },
  methods: {
    addTodo() {
      let newTodo = {
        id: Date.now(),
        name: this.newTodoName
      }
      this.todos.push(newTodo)
      this.newTodoName = ''
    },
    deleteTodo(index) {
      this.todos.splice(index, 1)
    }
  },
  watch: {
    newTodoName(newValue) {
      console.log('newValue', newValue);
      if(this.swearWords.includes(newValue.toLowerCase())){
        this.newTodoName = ''
        alert('You must never say ' + newValue + ' !!')
      }
    }
  }
};
</script>

<style>
ul {
  list-style: none;
  padding: 0;
  width: 200px;
  margin: 20px auto 0;
  background-color: #fff;
}
li {
  border: 1px solid;
  display: flex;
  margin-bottom: 10px;
}
li span {
  flex-grow: 1;
}
</style>
