<template>
  <div class="container" id="app">
    <h1>{{msg}}</h1>
    <hr>
    <div class="row" >
      <h2>Add Task</h2>
      <input type="number" v-model="Id" class="form-control" placeholder="Enter Id" >
      <input type="text" v-model="Title" class="form-control" placeholder="Enter Title" >
      <select class="form-control" v-model="Status">
        <option value="done">done</option>
        <option value="pending">pending</option>
      </select>
      <button @click="onAdd()" class="form-control btn btn-primary">Add Task</button>
    </div>
    <hr>
    <div class="row" >
      <table class="table">
        <th>Id</th>
        <th>Title</th>
        <th>Status</th>
        <th>Action</th>
      <!-- <tr v-for="(item,x) in tasks" > use this loop if you need index -->
      <tr v-for="(item,x) in tasks" >
        <td> {{item.Id}}</td>
        <td> {{item.Title}} </td>
      <!-- uncomment following td to use if and else-->
        <!-- <td v-if="item.Status=='done'" style="color:blue;" > {{item.Status}} </td>
        <td v-else style="color:red;" > {{item.Status}} </td> -->
        <!--how to apply css runtime and conditionally -->
        <td :class="{red:item.Status=='done',blue:item.Status=='pending'}" >{{item.Status}}</td>
        <td>
<button @click="onDelete(item)" type="button" class="btn btn-default" >
  <span class="glyphicon glyphicon-trash" aria-hidden="true"></span>
</button>
|
<button @click="onEdit(item)" type="button" class="btn btn-default" >
  <span class="glyphicon glyphicon-pencil" aria-hidden="true"></span>
</button>

        </td>
      </tr>
    </table>
    </div>

  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      msg: "Welcome to Your Vue.js App",
      Id: null,
      Title: "",
      Status: "pending",
      tasks: [
        { Id: 1, Title: "push your code to github", Status: "pending" },
        { Id: 2, Title: "Email to your manager", Status: "done" },
        { Id: 3, Title: "go for running", Status: "pending" }
      ]
    };
  },
  methods: {
    onDelete(item) {
      this.tasks.splice(this.tasks.indexOf(item), 1);
    },
    onEdit(item) {
      if (item.Status == "done") {
        item.Status = "pending";
      } else {
        item.Status = "done";
      }
    },
    onAdd() {
      var obj = { Id: this.Id, Title: this.Title, Status: this.Status };
      this.tasks.push(obj);
      this.Id = null;
      this.Title = "";
      this.Status = "pending";
    }
  }
};
</script>

<style lang="scss">
.red{
  color: red;
}
.blue{
  color: blue;
}
</style>
