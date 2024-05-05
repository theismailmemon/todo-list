<template>
  <div @click="cancelDelete" v-if="isModalOpen"
    class="fixed inset-0 z-[100] flex items-center justify-center bg-gray-900 bg-opacity-50">
    <div class="bg-white max-w-auto max-w-full mx-6 p-6 rounded-lg shadow-xl" @click.stop>
      <h2 class="text-xl text-gray-700 font-semibold mb-4">Confirm Deletion</h2>
      <p>Are you sure you want to delete "{{ todoToDelete.name }}"?</p>
      <div class="flex justify-end mt-4">
        <button @click="cancelDelete" class="px-4 py-2 bg-red-500 text-white hover:opacity-80 transition ease-in-out duration-300 rounded-md mr-2">Cancel</button>
        <button @click="confirmDelete"
          class="px-4 py-2 w-20 flex justify-center items-center bg-green-500 text-white hover:opacity-80 transition ease-in-out duration-300 rounded-md"
          :class="{ 'opacity-60 pointer-events-none': loadingAnimation }">
          <span v-if="!loadingAnimation">Delete</span>
          <div class="flex flex-row space-x-4" v-else>
            <div class="w-6 h-6 rounded-full animate-spin border border-solid border-white border-t-transparent"></div>
          </div>
        </button>

      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loadingAnimation: false
    }
  },
  props: {
    isModalOpen: {
      type: Boolean,
      default: false
    },
    todoToDelete: Object
  },
  methods: {
    cancelDelete() {
      this.$emit('cancel-delete');
    },
    confirmDelete() {
      this.loadingAnimation = true;
      setTimeout(() => {
        this.loadingAnimation = false;
        this.$emit('confirm-delete', this.todoToDelete);
      }, 1000); // Replace 1000 with the desired delay in milliseconds
    }

  }
}
</script>