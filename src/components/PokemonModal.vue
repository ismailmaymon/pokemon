<template>
  <div>
    <transition name="modal-fade" appear>
      <div
        v-if="isModalOpen"
        class="fixed inset-0 z-50 flex sm:items-center justify-end bg-black bg-opacity-50"
        @click="closeModal"
        @touchstart="handleTouchStart"
        @touchmove="handleTouchMove"
        @touchend="handleTouchEnd"
      >
        <div
          class="bg-blue-950 sm:max-w-[450px] w-full sm:ml-0 ml-14 !h-full overflow-y-auto"
          @click.stop
        >
          <div class="h-[50%] px-5">
            <div class="flex items-center justify-between pt-10">
              <h2 class="text-white text-3xl font-medium">
                {{ pokemonDeatil.name }}
              </h2>
              <h2 class="text-white">
                # <span v-if="pokemonDeatil.id <= 9">0</span
                ><span>{{ pokemonDeatil.id }}</span>
              </h2>
            </div>
            <div class="flex justify-start mt-5 gap-2">
              <h2
                class="bg-blue-900 text-white rounded-full px-[12px] shadow py-[2px]"
              >
                {{ pokemonDeatil.firstName }}
              </h2>
              <h2
                class="bg-blue-900 text-white rounded-full px-[12px] shadow py-[2px]"
              >
                {{ pokemonDeatil.secondName }}
              </h2>
            </div>
            <div class="flex items-center h-[calc(100%-120px)]">
              <img
                :src="pokemonDeatil.imageUrl"
                alt=""
                class="sm:w-40 w-36 mx-auto"
              />
            </div>
          </div>
          <div
            class="bg-white sm:rounded-t-3xl rounded-t-xl h-[50%] px-5 pt-10"
          >
            <div class="max-w-48">
              <h1 class="flex justify-between mt-4 text-lg">
                <span class="text-blue-950 font-semibold">Experience:</span>
                <span class="text-blue-900 font-semibold">64 EXP</span>
              </h1>
              <h1 class="flex justify-between mt-4 text-lg">
                <span class="text-blue-950 font-semibold">Height:</span>
                <span class="text-blue-900 font-semibold">7 m</span>
              </h1>
              <h1 class="flex justify-between mt-4 sm:text-lg">
                <span class="text-blue-950 font-semibold">Weight:</span>
                <span class="text-blue-900 font-semibold">69 Kg</span>
              </h1>
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
    pokemonDeatil: Object,
    isModalOpen: Boolean,
  },
  watch: {
    isModalOpen(newValue) {
      if (newValue) {
        document.body.classList.add("overflow-hidden");
      } else {
        document.body.classList.remove("overflow-hidden");
      }
    },
  },
  data() {
    return {
      touchStartX: 0,
    };
  },
  methods: {
    closeModal() {
      this.$emit("closeModal");
      document.body.classList.remove("overflow-hidden");
    },
    handleTouchStart(event) {
      this.touchStartX = event.touches[0].clientX;
    },
    handleTouchMove(event) {
      const touchMoveX = event.touches[0].clientX;
      if (touchMoveX - this.touchStartX > 50) {
      }
    },
    handleTouchEnd(event) {
      const touchEndX = event.changedTouches[0].clientX;
      if (touchEndX - this.touchStartX > 50) {
        this.closeModal();
      }
    },
  },
};
</script>
