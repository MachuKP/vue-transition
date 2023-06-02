<script setup>
import { ref } from "vue";

const todos = ref([
  { text: "share knowledge", id: crypto.randomUUID() },
  { text: "pretent to be working", id: crypto.randomUUID() },
]);
const newTodo = ref("");

const emit = defineEmits(["invalidValue"]);

const addTodo = () => {
  if (newTodo.value) {
    const id = crypto.randomUUID();
    todos.value = [{ text: newTodo.value, id }, ...todos.value];
    newTodo.value = "";
  } else {
    emit("invalidValue");
  }
};

const deleteTodo = (id) => {
  todos.value = todos.value.filter((todo) => todo.id !== id);
};
</script>

<template>
  <div class="todos">
    <input
      type="text"
      v-model="newTodo"
      @keypress.enter="addTodo"
      placeholder="Add a new todo..."
    />
    <transition name="switch" mode="out-in">    
      <div v-if="todos.length">
        <transition-group tag="ul" name="list" appear>
          <li v-for="todo in todos" :key="todo.id" @click="deleteTodo(todo.id)">
            {{ todo.text }}
          </li>
        </transition-group>
      </div>
      <div v-else>Time to pretent to be waking up</div>
    </transition>
  </div>
</template>

<style scoped>
.list-enter-from {
  transform: scale(0.6);
  opacity: 0;
}
.list-leave-to {
  transform: scale(0.6);
  opacity: 0;
}
.list-enter-active {
  transition: all 0.4s ease;
}
.list-leave-active {
  transition: all 0.4s ease;
  position: absolute;
}
.list-move {
  transition: all 0.3s ease;
}
.switch-enter-from,
.switch-leave-to {
  transform: translateY(-10px);
  opacity: 0;
}
.switch-enter-active,
.switch-leave-active {
  transition: all 0.3s ease
}
.todos {
  max-width: 400px;
  margin: 20px auto;
  position: relative;
}
input {
  width: 100%;
  padding: 12px;
  border: 1px solid #eee;
  border-radius: 10px;
  box-sizing: border-box;
  margin-bottom: 20px;
}
.todos ul {
  position: relative;
  padding: 0;
}
.todos li {
  list-style-type: none;
  display: block;
  margin-bottom: 10px;
  padding: 10px;
  background: white;
  box-shadow: 1px 3px 5px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  width: 100%;
  box-sizing: border-box;
}
.todos li:hover {
  cursor: pointer;
}
</style>
