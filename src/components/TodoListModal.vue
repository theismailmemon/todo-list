<template>
  <div>
    <transition name="modal-fade" appear>
      <div v-if="isModalOpen" class="fixed flex justify-center inset-0 z-50 items-center bg-black bg-opacity-50"
        @click="$emit('closeModal')">
        <div class="bg-blue-950 sm:w-1/4 w-full sm:mx-0 mx-6 sm:h-64 h-52 rounded-2xl" @click.stop>
          <div class="border-white border-b flex justify-between px-5 py-3">
            <h1 class="text-white text-xl">Add Todo</h1>
            <svg @click="$emit('closeModal')" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
              stroke-width="1.5" stroke="currentColor"
              class="text-white w-6 h-6 cursor-pointer hover:opacity-80 transition ease-in-out duration-300">
              <path stroke-linecap="round" stroke-linejoin="round" d="M6 18 18 6M6 6l12 12" />
            </svg>
          </div>
          <div class="px-5 mt-5">
            <div>
              <input v-model="inputAdd" type="text"
                class="bg-white shadow w-full focus:outline-none text-blue-950 px-4 py-2 rounded-lg placeholder:text-blue-950 text-lg"
                placeholder="Add Todo">
            </div>
            <div class="flex justify-end mt-5">
              <button @click="handleAdd"
                class="bg-white px-4 py-2 text-blue-950 rounded-lg cursor-pointer hover:opacity-80 transition ease-in-out duration-300">
                Add
              </button>
            </div>
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  props: {
    addTodo: Function, // Corrected to Function type
    isModalOpen: Boolean,
  },
  data() {
    return {

      inputAdd: "" // Moved inside data function
    };
  },
  methods: {
    handleAdd() {
      if (this.inputAdd.length <= 0) { } else {
        this.addTodo(this.inputAdd);
        this.inputAdd = ""; // Clear input field after adding todo
        this.showError = false; // Reset error state after successfully adding todo
        this.$emit('closeModal')
      }
    }
  },
};
</script>

<style scoped>
.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: opacity 0.2s;
}

.modal-fade-enter,
.modal-fade-leave-to {
  opacity: 0;
}
</style>
