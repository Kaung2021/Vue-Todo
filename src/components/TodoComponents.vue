<template>
  <div class="container">
    <h1 class="text-cente mb-5">Todo by Vue</h1>
    <!-- Input Field -->
    <div class="d-flex">
      <input type="text" class="form-control" v-model="task" />
      <button class="btn btn-success rounded-0" @click="SubmitInput">
        Input
      </button>
    </div>
    <!-- Table -->
    <table class="table table-bordered">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col">Status</th>
          <th scope="col">#</th>
          <th scope="col">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <th scope="row" :class="{ finished: task.status === 'finished' }">
            {{ task.name }}
          </th>
          <td style="width: 120px">
            <span
              @click="ChangeStatus(index)"
              class="pointer"
              :class="{
                'text-danger': task.status === 'to-do',
                'text-success': task.status === 'finished',
                'text-warning': task.status === 'in-progress',
              }"
            >
              {{ firstChar(task.status) }}
            </span>
          </td>
          <td>
            <div @click="editTodo(index)"><i class="fa fa-pen"></i></div>
          </td>
          <td>
            <div @click="deleteTodo(index)"><i class="fa fa-trash"></i></div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
export default {
  name: "TodoComponents",
  data() {
    return {
      task: "",
      editedTodo: null,
      avaliableStatus: ["todo", "in-progress", "finished"],
      tasks: [
        {
          name: "My Brother is still trying to understand how to read the log in Math",
          status: "in-process",
        },
        {
          name: "I am also practice how to create the todoList project with Vuejs",
          status: "in-process",
        },
        {
          name: "I still care about EiPayy even what she hurt to me",
          status: "in-process",
        },
      ],
    };
  },
  methods: {
    //   SubmitINput
    SubmitInput() {
      if (this.task.length === 0) return "Invaild message";
      if (this.editedTodo === null) {
        //    We are going to add data using push method

        this.tasks.push({
          name: this.task,
          status: "todo",
        });
      } else {
        this.tasks[this.editedTodo].name = this.task;
        this.editedTodo = null;
      }
      //  lets make an empty string
      this.task = "";
    },
    // deleteInput
    deleteTodo(index) {
      this.tasks.splice(index, 1);
    },
    // For editing
    editTodo(index) {
      this.task = this.tasks[index].name;
      this.editedTodo = index;
    },
    // Change the status
    ChangeStatus(index) {
      let newIndex = this.avaliableStatus.indexOf(this.tasks[index].status);
      if (++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.avaliableStatus[newIndex];
    },
    // Change the first letter to upperLetter
    firstChar(str) {
      return str.charAt(0).toUpperCase() + str.substring(1);
    },
  },
};
</script>
<style scoped>
.pointer {
  cursor: pointer;
}
.finished {
  text-decoration: line-through;
}
</style>
