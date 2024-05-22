<template>
  <div>
    <transition name="modal-fade" appear>
      <div v-if="isModalOpen" class="fixed inset-0 z-50 flex items-center justify-end bg-black bg-opacity-50"  @click="$emit('closeModal')">
        <div class="bg-white sm:max-w-[420px] w-full sm:ml-0 ml-10 h-full" @click.stop>
          <div class="border-blue-950 border-b flex justify-between px-5 py-3">
            <h1 class="text-blue-950 text-xl">Add Todo</h1>
            <svg @click="$emit('closeModal')" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
              stroke-width="1.5" stroke="currentColor"
              class="text-blue-950 w-6 h-6 cursor-pointer hover:opacity-80 transition ease-in-out duration-300">
              <path stroke-linecap="round" stroke-linejoin="round" d="M6 18 18 6M6 6l12 12" />
            </svg>
          </div>
          <div class="px-5 mt-5">
            <div>
              <input v-model="inputAdd" type="text"
                class="bg-blue-950 shadow w-full focus:outline-none text-white px-4 py-2 rounded-lg placeholder:text-white text-lg"
                placeholder="Add Todo">
            </div>
          
          </div>
          <div class="fixed bottom-5 px-5 border-t pt-3 w-[22%]">
             <div>
              <button @click="handleAdd"
                class="bg-blue-950 px-4 py-2 w-full text-white rounded-lg cursor-pointer hover:opacity-80 transition ease-in-out duration-300">
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
      if (this.inputAdd.length === 0) { } else {
        this.addTodo.push(
          {
          name: this.inputAdd,
          isTrueRecycle: true
        },
        );
        this.inputAdd = ""; // Clear input field after adding todo
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
