<template>
  <div class="relative">
    <button class="z-10 relative flex items-center focus:outline-none select-none" @click="open = !open">
      <slot name="button"></slot>
    </button>

    <!-- to close when clicked on space around it in desktop-->
    <button class="fixed inset-0 h-full w-full cursor-default focus:outline-none" v-if="open" @click="open = false" tabindex="-1"></button>
    <!--dropdown content: desktop-->
    <transition
      enter-active-class="transition-all duration-200 ease-out"
      leave-active-class="transition-all duration-750 ease-in"
      enter-class="opacity-0 scale-75"
      enter-to-class="opacity-100 scale-100"
      leave-class="opacity-100 scale-100"
      leave-to-class="opacity-0 scale-75"
    >
      <div class="hidden md:block absolute shadow-lg border w-48 rounded py-1 px-2 text-sm mt-4 bg-white" :class="placement === 'right' ? 'right-0' : 'left-0'" v-if="open">
        <slot name="content"></slot>
      </div>
    </transition>

    <!--dropdown content: mobile-->
    <transition
      enter-active-class="transition-all duration-200 ease-out"
      leave-active-class="transition-all duration-750 ease-in"
      enter-class="opacity-0 scale-75"
      enter-to-class="opacity-100 scale-100"
      leave-class="opacity-100 scale-100"
      leave-to-class="opacity-0 scale-75"
    >
      <div class="md:hidden fixed inset-x-0 bottom-0 bg-white w-full z-20 px-2 py-2 shadow-2xl leading-loose" v-if="open">
        <slot name="content"></slot>
      </div>
    </transition>
    <!-- to close when clicked on space around it in mobile-->
    <div class="md:hidden fixed w-full h-full inset-0 bg-gray-900 opacity-50 z-10" @click="open = false" v-if="open"></div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        open: false,
      };
    },
    props: {
      placement: {
        type: String,
        default: "right",
        validator: (value) => ["right", "left"].indexOf(value) !== -1,
      },
    },
    mounted() {
      const onEscape = (e) => {
        if (e.key === "Esc" || e.key === "Escape") {
          this.open = false;
        }
      };

      document.addEventListener("keydown", onEscape);

      this.$once("hook:beforeDestroy", () => {
        document.removeEventListener("keydown", onEscape);
      });
    },
  };
</script>
