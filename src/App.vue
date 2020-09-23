<template>
  <div id="app">
    <h1>ToDoリスト</h1>
    <input type="radio" name="type" />すべて
    <input type="radio" name="type" />作業中
    <input type="radio" name="type" />完了
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>コメント</th>
          <th>状態</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(todo, index) in todos" :key="todo.id">
          <td>{{ index }}</td>
          <td>{{ todo.comment }}</td>
          <td>
            <button @click="changeStatus(index)">{{ todo.status }}</button>
          </td>
          <th>
            <button @click="deleteTask(index)">削除</button>
          </th>
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
      newTask: "",
      todos: []
    };
  },
  methods: {
    addTask() {
      if (this.newTask === "") {
        alert("未入力です");
      } else {
        this.todos.push({ comment: this.newTask, status: "作業中" });
        this.newTask = "";
      }
    },
    deleteTask(index) {
      this.todos.splice(index, 1);
    },
    changeStatus(index) {
      if (this.todos[index].status === "作業中") {
        this.todos[index].status = "完了";
      } else if (this.todos[index].status === "完了") {
        this.todos[index].status = "作業中";
      }
    }
  }
};
</script>

