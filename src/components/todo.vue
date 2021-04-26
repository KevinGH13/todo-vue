<template>
  <section class="section">
    <div class="container" id="todo">
      <div>
        <h1>TO-DO</h1>
      </div>
      <div class="row">
        <div class="col-sm">
          <div class="input-group input-group-md">
            <input
              type="text"
              class="form-control"
              placeholder="Add new task"
              v-model="newTodo"
              @keyup.enter="addTodo"
            />
          </div>
        </div>
      </div>
      <br />
      <div class="row">
        <div class="col-sm">
          <div class="card">
            <div class="card-body" v-for="todo in todosFiltered" :key="todo.id">
              <div class="form-check">
                <input
                  class="form-check-input"
                  type="checkbox"
                  v-model="todo.done"
                />
                <label
                  class="form-check-label"
                  for="flexCheckDefault"
                  v-bind:class="{ done: todo.done }"
                >
                  {{ todo.text }}
                </label>
              </div>
            </div>
            <hr />
            <div class="row">
              <div class="col-3"></div>
              <div class="col-6">
                <div class="btn-group" role="group">
                  <button
                    type="button"
                    class="btn btn-outline-primary"
                    :class="{ active: filter == 'all' }"
                    @click="filter == 'all'"
                  >
                    All
                  </button>
                  <button
                    type="button"
                    class="btn btn-outline-primary"
                    :class="{ active: filter == 'active' }"
                    @click="filter == 'active'"
                  >
                    Active
                  </button>
                  <button
                    type="button"
                    class="btn btn-outline-primary"
                    :class="{ active: filter == 'done' }"
                    @click="filter == 'done'"
                  >
                    Complete
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>


<script>
export default {
  name: "todo",
  data() {
    return {
      newTodo: "",
      todoText: "",
      todoCount: "",
      idTodo: 0,
      filter: "all",
      todos: [],
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.idTodo,
        text: this.newTodo,
        done: false,
      });

      this.newTodo = "";
      this.idTodo++;
      this.todoCount++;
    },
  },
  computed: {
    todosFiltered() {
      console.log("in");
      if (this.filter == "all") {
        return this.todos;
      } else if (this.filter == "active") {
        return this.todos.filter((todo) => !todo.done);
      } else if (this.filter == "completed") {
        console.log(this.todos.filter((todo) => todo.done));
        return this.todos.filter((todo) => todo.done);
      }
      return this.todos;
    },
  },
};
</script>
<style>
.done {
  text-decoration: line-through;
  color: grey;
}
</style>
