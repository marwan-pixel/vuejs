<template>
  <div class="container">
    <img alt="Vue logo" src="./assets/logo.png" />
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <h1>Hello World</h1>
    <p ref="pElementRef">Hello</p>
    <TestWeb :msg="greeting" />
    <div class="d-grid gap-2 d-md-flex justify-content-md-center mb-3" id="app">
      <button class="btn btn-primary" v-on:click="increment">Increment</button>
      <button class="btn btn-warning" @click="decrement">Decrement</button>
      <button class="btn btn-danger" @click="reset">Reset Count</button>
    </div>
    <p>You have clicked: {{ count }} times!</p>

    <input :value="text" @input="onInput" placeholder="Type here" />
    <p>{{ text }}</p>

    <hr />

    <p class="fw-bold">Toggle Button</p>
    <button class="btn-success btn" @click="toggle">Click</button>
    <p class="fw-bold h5 mt-4" v-if="awesome">Awesome!!</p>
    <p class="fw-bold h5 mt-4" v-else>Oh No 😢!!</p>

    <hr />
    <p class="h5 fw-bold">Simple To Do List</p>
    <div class="container">
      <div class="row justify-content-md-center">
        <div class="col col-lg-4 mb-3">
          <table class="table table-striped table-hover">
            <tbody>
              <tr v-for="todo in filteredTodos" :key="todo.id">
                <td>
                  <input
                    type="checkbox"
                    class="form-check-input"
                    v-model="todo.done"
                  />
                </td>
                <td>
                  <span :class="{ done: todo.done }">{{ todo.text }}</span>
                </td>
                <td>
                  <button @click="removeTodo(todo)" class="btn btn-danger">
                    Delete
                  </button>
                </td>
              </tr>
            </tbody>
          </table>
          <button
            class="btn btn-danger"
            @click="hideCompleted = !hideCompleted"
          >
            {{ hideCompleted ? "Show All" : "Hide Completed" }}
          </button>
        </div>
      </div>
      <div class="row justify-content-md-center">
        <div class="col col-lg-4">
          <form @submit.prevent="addTodo">
            <label for="input" class="form-label">Insert To Do</label>
            <div class="input-group mb-3">
              <input class="form-control" id="input" v-model="newTodo" />
            </div>
            <button class="btn btn-primary">Submit</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
// import HelloWorld from './components/HelloWorld.vue'
import { computed, ref, onMounted } from "vue";
import TestWeb from './components/TestWeb.vue';
const pElementRef = ref(null);
onMounted(() => {
  pElementRef.value.textContent = "mounted!";
  console.log("onMounted")
});

const greeting = ref("Hello from parent");

let id = 0;

const newTodo = ref("");
const todos = ref([
  { id: id++, text: "Learn HTML", done: true },
  { id: id++, text: "Learn Javascript", done: false },
  { id: id++, text: "Learn Vue", done: true },
]);
const hideCompleted = ref(false);

const filteredTodos = computed(() => {
  return hideCompleted.value ? todos.value.filter((t) => !t.done) : todos.value;
});

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false });
  newTodo.value = "";
}

function removeTodo(todo) {
  todos.value = todos.value.filter((el) => el !== todo);
}

const text = ref("");
const count = ref(0);
const awesome = ref(true);

function onInput(e) {
  text.value = e.target.value;
}

function increment() {
  count.value++;
}

function decrement() {
  count.value--;
}

function reset() {
  count.value = 0;
}

function toggle() {
  awesome.value = !awesome.value;
}
// export default {
//   name: 'App',
//   data: function() {
//     return {
//       count: 0,
//     };
//   },
//   methods: {
//     increment: function () {
//       this.count++;
//     },
//     decrement: function () {
//       this.count--;
//     },
//     reset: function() {
//       this.count = 0;
//     },

//   }
// }
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.done {
  text-decoration: line-through;
}
</style>
