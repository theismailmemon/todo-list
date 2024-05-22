<template>
  <div>
    <transition name="modal-fade" appear>
      <div @click="$emit('closeModal')" @touchstart="handleTouchStart" @touchmove="handleTouchMove"
        @touchend="handleTouchEnd" v-if="isModalOpen"
        class="fixed inset-0 z-50 flex items-center justify-end bg-black bg-opacity-50">
        <div class="bg-white sm:max-w-[450px] w-full sm:ml-0 ml-14 h-full" @click.stop>
          <div class="h-full">
            <div class="border-b flex justify-between items-center px-5 py-3">
              <h1 class="text-blue-950 text-2xl">Add Todo</h1>
              <svg @click="$emit('closeModal')" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
                stroke-width="1.5" stroke="currentColor"
                class="text-blue-950 w-6 h-6 cursor-pointer hover:opacity-80 transition ease-in-out duration-300">
                <path stroke-linecap="round" stroke-linejoin="round" d="M6 18 18 6M6 6l12 12" />
              </svg>
            </div>
            <div class=" mt-5 h-full">
              <div class="px-5">
                <input v-model="inputAdd" type="text"
                  class="border w-full focus:outline-none px-4 py-2 rounded-lg  text-lg" placeholder="Type a Todo">
              </div>
              <div class="w-full sm:h-[calc(100%-145px)] h-[calc(100%-140px)] flex items-end">
<div class="border-t w-full px-5 sm:pt-5 pt-4">
  <button @click="handleAdd"
                  class="bg-blue-950 sm:text-xl text-lg px-4 py-2 w-full text-white rounded-lg cursor-pointer hover:opacity-80 transition ease-in-out duration-300">
                  Add
                </button>
</div>
              </div>
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
    addTodo: Function,
    isModalOpen: Boolean,
  },
  data() {
    return {
      inputAdd: ""
    };
  },
  methods: {
    handleTouchStart(event) {
      this.touchStartX = event.touches[0].clientX;
    },
    handleTouchMove(event) {
      const touchMoveX = event.touches[0].clientX;
      if (touchMoveX - this.touchStartX > 50) {
        // If sliding right, hide swipe indicator
      }
    },
    handleTouchEnd(event) {
      const touchEndX = event.changedTouches[0].clientX;
      if (touchEndX - this.touchStartX > 50) {
        // If the touch ended with a left swipe (positive difference in X coordinates)
        this.$emit('closeModal');
      }
    },
    handleAdd() {
      if (this.inputAdd.length === 0) { } else {
        this.addTodo.push(
          {
            name: this.inputAdd,
            isTrueRecycle: true
          },
        );
        this.inputAdd = "";
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
