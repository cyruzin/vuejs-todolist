<template>
  <div>
    <input type="text" placeholder="Add a task" v-model="task">
    <button v-on:click="addTodo">ADD</button>

    <div class="container" v-if="todo.length > 0">
      <ul class="todo">
        <li
          class="list"
          v-for="t in todo"
          :key="t.id"
          v-bind:class="{completed: t.completed}"
          v-on:click="markTodo(t)"
        >
          {{ t.name }}
          <button class="remove" v-on:click="removeTodo(t)">x</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "ToDoList",
  data() {
    return {
      task: null,
      todo: []
    };
  },
  methods: {
    addTodo: function() {
      if (this.task === null) return false;
      this.todo = [
        ...this.todo,
        { id: Date.now(), name: this.task, completed: false }
      ];
      this.task = null;
    },
    markTodo: function(task) {
      this.todo.find(t => {
        if (t.id === task.id) t.completed = !t.completed;
      });
    },
    removeTodo: function(task) {
      this.todo = this.todo.filter(t => t.id !== task.id);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
input[type="text"] {
  width: 30%;
  border-radius: 4px;
  border: 1px solid #ccc;
  padding: 10px;
}

button {
  border-radius: 4px;
  padding: 10px;
  margin-left: 5px;
  background: springgreen;
}

.container {
  display: grid;
  justify-content: center;
  align-items: center;
}

.todo {
  display: grid;
  grid-template-columns: 1fr;
  padding-top: 2rem;
  font-size: 1.4rem;
  width: 20rem;
}

.remove {
  border-radius: 4px;
  padding: 5px;
  margin-left: 5px;
  background: salmon;
  cursor: pointer;
  width: 2rem;
  text-justify: end;
}

.list {
  cursor: pointer;
}
.completed {
  text-decoration: line-through;
}
</style>
