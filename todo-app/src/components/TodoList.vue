<template>
  <div>
    <p class="tasks">
      Completed Tasks:
      {{
        todos.filter(todo => {
          return todo.done === true;
        }).length
      }}
    </p>
    <p class="tasks">
      Pending Tasks:
      {{
        todos.filter(todo => {
          return todo.done === false;
        }).length
      }}
    </p>
    <div v-for="(todo, index) in todos" :key="index">
      <todo
        v-on:delete-todo="deleteTodo"
        v-on:complete-todo="completeTodo"
        v-bind:todo="todos[index]"
      ></todo>
    </div>
  </div>
</template>

<script type="text/javascript">
import sweetalert from "sweetalert";
import Todo from "./Todo";
export default {
  props: ["todos"],
  components: {
    Todo
  },
  methods: {
    deleteTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos.splice(todoIndex, 1);
      sweetalert("Deleted!", "Your To-Do has been deleted.", "success");
      // sweetalert(
      //   {
      //     title: "Are you sure?",
      //     text: "This To-Do will be permanently deleted!",
      //     type: "warning",
      //     showCancelButton: true,
      //     confirmButtonColor: "#DD6B55",
      //     confirmButtonText: "Yes, delete it!",
      //     closeOnConfirm: false
      //   },
      //   () => {
      //     const todoIndex = this.todos.indexOf(todo);
      //     this.todos.splice(todoIndex, 1);
      //     sweetalert("Deleted!", "Your To-Do has been deleted.", "success");
      //   }
      // );
    },
    completeTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos[todoIndex].done = true;
      sweetalert("Success!", "To-Do completed!", "success");
    }
  }
};
</script>

<style scoped>
p.tasks {
  text-align: center;
}
</style>
