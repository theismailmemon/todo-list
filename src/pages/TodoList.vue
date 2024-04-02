<script>
import todoListModal from '../components/TodoListModal.vue'
export default {
  components: {
    todoListModal
  },
  data() {
    return {
      isModalOpen: false,
      todoList: [
        {
          name: "Prayer",
          isTrueRecycle: true
        },
        {
          name: "School",
          isTrueRecycle: true
        },
        {
          name: "Colleage",
          isTrueRecycle: true
        },
        {
          name: "University",
          isTrueRecycle: true
        },
        {
          name: "Academy",
          isTrueRecycle: true
        },
      ]
    }
  },
  methods: {
    deleteTodo(index) {
      this.todoList.splice(index, 1);
    },
    addTodo(inputAdd) {
      this.todoList.push({
        name: inputAdd,
        isTrueRecycle: true
      });
    }
  }
}
</script>
<template>
  <div class="relative h-screen">
    <div class="mx-auto sm:container sm:py-24 py-5 px-5">
      <h1 class="sm:text-3xl text-2xl font-medium text-blue-950">Todo List</h1>
      <div class="sm:mt-6">
        <div class="bg-blue-950 shadow w-full rounded-xl px-6 sm:py-3 py-2 my-5 flex justify-between"
          v-for="(item, index) in todoList" :key="index">
          <div class="flex items-center gap-5">
            <input type="checkbox" name="" id="" class="h-4 w-4 cursor-pointer" @change="item.isTrueRecycle = false"
              v-if="item.isTrueRecycle === true">
            <h1 v-if="item.isTrueRecycle === true" class="text-white text-2xl">{{ item.name }}</h1>
            <strike v-if="item.isTrueRecycle === false" class="text-white text-2xl">{{ item.name }}</strike>
          </div>
          <div class="flex items-center gap-3">
            <svg @click="item.isTrueRecycle = true" v-if="item.isTrueRecycle === false"
              xmlns="http://www.w3.org/2000/svg"
              class="text-white h-5 w-5 cursor-pointer transition ease-in-out duration-300 hover:opacity-80 icon icon-tabler icon-tabler-refresh"
              viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" fill="none" stroke-linecap="round"
              stroke-linejoin="round">
              <path stroke="none" d="M0 0h24v24H0z" fill="none" />
              <path d="M20 11a8.1 8.1 0 0 0 -15.5 -2m-.5 -4v4h4" />
              <path d="M4 13a8.1 8.1 0 0 0 15.5 2m.5 4v-4h-4" />
            </svg>

            <svg @click="deleteTodo(index)" xmlns="http://www.w3.org/2000/svg"
              class="text-white h-5 w-5 cursor-pointer transition ease-in-out duration-300 hover:opacity-80 icon icon-tabler icon-tabler-trash"
              viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" fill="none" stroke-linecap="round"
              stroke-linejoin="round">
              <path stroke="none" d="M0 0h24v24H0z" fill="none" />
              <path d="M4 7l16 0" />
              <path d="M10 11l0 6" />
              <path d="M14 11l0 6" />
              <path d="M5 7l1 12a2 2 0 0 0 2 2h8a2 2 0 0 0 2 -2l1 -12" />
              <path d="M9 7v-3a1 1 0 0 1 1 -1h4a1 1 0 0 1 1 1v3" />
            </svg>
          </div>
        </div>
      </div>
    </div>
    <div>
      <todoListModal :isModalOpen="isModalOpen" @closeModal="isModalOpen = false" :addTodo="addTodo" />
    </div>
    <div class="pt-10">
      <div class="fixed bottom-16 sm:right-16 right-6">
        <div class="bg-blue-950 p-1 rounded-lg cursor-pointer" @click="isModalOpen = true">
          <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-plus text-white h-8 w-8"
            viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" fill="none" stroke-linecap="round"
            stroke-linejoin="round">
            <path stroke="none" d="M0 0h24v24H0z" fill="none" />
            <path d="M12 5l0 14" />
            <path d="M5 12l14 0" />
          </svg>
        </div>
      </div>
    </div>
  </div>
</template>
