<template>
  <div id="app">
    <h1>ToDoリスト</h1>
    <input type="radio" name="type" v-model="radio" :value="status.all" />すべて
    <input type="radio" name="type" v-model="radio" :value="status.doing" />作業中
    <input type="radio" name="type" v-model="radio" :value="status.done" />完了
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>コメント</th>
          <th>状態</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="todo in generateTodos" :key="todo.id">
          <td>{{ todo.id }}</td>
          <td>{{ todo.comment }}</td>
          <td><button @click="changeStatus(todo.id)">{{ todo.status }}</button></td>
          <td><button @click="deleteTask(todo.id)">削除</button></td>
        </tr>
      </tbody>
    </table>
    <h2>新規タスクの追加</h2>
    <input id="task" type="text" v-model="newTask" />
    <button id="add" @click="addTask()">追加</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      newTask: '',
      taskId: 0,
      radio: 'すべて',
      status: {
        all: 'すべて',
        doing: '作業中',
        done: '完了'
      }      
    };
  },
  methods: {
    setTaskId() {
      this.todos.forEach((todo, index) => {
        todo.id = index;
      });
    },
    addTask() {
      if (!this.newTask) {
        alert('未入力です');
        return
      }
      this.todos.push({
        id: this.taskId,
        comment: this.newTask,
        status: this.status.doing
      });
      this.taskId++;
      this.newTask = '';
      this.setTaskId();
    },
    deleteTask(id) {
      this.todos.splice(id, 1);
      this.setTaskId();
    },
    changeStatus(id) {
      if (this.todos[id].status === this.status.doing) {
        this.todos[id].status = this.status.done;
      } else if (this.todos[id].status === this.status.done) {
        this.todos[id].status = this.status.doing;
      }
    },
  },
  computed: {
    generateTodos: function() {
      if (this.radio === this.status.all) {
        return this.todos;
      } else if (this.radio === this.status.doing) {
        const newTodos = this.todos.filter(todo => todo.status === this.status.doing);
        return newTodos;
      } else {
        const newTodos = this.todos.filter(todo => todo.status === this.status.done);
        return newTodos;
      }
    }
  }
};
</script>

