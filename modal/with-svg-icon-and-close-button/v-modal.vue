<template>
  <div class="fixed w-full h-full top-0 left-0 flex items-center justify-center z-10" v-if="open">
    <div class="absolute w-full h-full bg-gray-900 opacity-50" @click="close"></div>

    <div class="absolute max-h-full" :class="maxWidth">
      <div class="container bg-white overflow-hidden md:rounded">
        <div class="px-4 py-4 flex justify-between items-start">
          <div class="mr-4">
            <svg class="fill-current h-5 md:h-6 w-5 md:w-6 md:mr-1" xmlns="http://www.w3.org/2000/svg" :class="color"
                 viewBox="0 0 20 20">
              <path v-if="type === 'info'"
                    d="M2.93 17.07A10 10 0 1 1 17.07 2.93 10 10 0 0 1 2.93 17.07zm12.73-1.41A8 8 0 1 0 4.34 4.34a8 8 0 0 0 11.32 11.32zM9 11V9h2v6H9v-4zm0-6h2v2H9V5z"/>
              <path v-if="type === 'warning'"
                    d="M2.93 17.07A10 10 0 1 1 17.07 2.93 10 10 0 0 1 2.93 17.07zm12.73-1.41A8 8 0 1 0 4.34 4.34a8 8 0 0 0 11.32 11.32zM9 5h2v6H9V5zm0 8h2v2H9v-2z"/>
              <path v-if="type === 'success'"
                    d="M2.93 17.07A10 10 0 1 1 17.07 2.93 10 10 0 0 1 2.93 17.07zm12.73-1.41A8 8 0 1 0 4.34 4.34a8 8 0 0 0 11.32 11.32zM6.7 9.29L9 11.6l4.3-4.3 1.4 1.42L9 14.4l-3.7-3.7 1.4-1.42z"/>
              <path v-if="type === 'danger'"
                    d="M0 10a10 10 0 1 1 20 0 10 10 0 0 1-20 0zm16.32-4.9L5.09 16.31A8 8 0 0 0 16.32 5.09zm-1.41-1.42A8 8 0 0 0 3.68 14.91L14.91 3.68z"/>
            </svg>
          </div>

          <div class="max-h-full">
            <div class="flex justify-between items-center mb-2">
              <h3 class="font-semibold" :class="color">{{ title }}</h3>

              <div @click="close"
                   class="text-2xl hover:text-gray-600 text-gray-500 cursor-pointer select-none flex leading-none">
                &#215;
              </div>
            </div>

            <!-- Content Slot-->
            <slot></slot>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        open: true
      };
    },
    props: {
      type: {
        type: String,
        default: 'info'
      },
      title: {
        type: String,
        default: ''
      },
      header: {
        type: String,
        required: false,
        default: ''
      },
      width: {
        type: String,
        default: 'full',
        validator: (value) => ['xs', 'sm', 'md', 'lg', 'full'].indexOf(value) !== -1,
      }
    },
    methods: {
      close() {
        this.open = false;
        this.$emit("close");
      }
    },
    computed: {
      maxWidth() {
        switch (this.width) {
          case 'xs':
            return 'max-w-lg';
          case 'sm':
            return 'max-w-xl';
          case 'md':
            return 'max-w-2xl';
          case 'lg':
            return 'max-w-3xl';
          case 'full':
            return 'max-w-full';
        }
      },
      shade() {
        switch (this.type) {
          case "info":
            return "gray";
          case "warning":
            return "yellow";
          case "success":
            return "teal";
          case "danger":
            return "red";
        }
      },
      color() {
        return `text-${this.shade}-600`;
      },
    },
    mounted() {
      const onEscape = (e) => {
        if (e.key === "Esc" || e.key === "Escape") {
          this.close();
        }
      };

      document.addEventListener("keydown", onEscape);

      this.$once("hook:beforeDestroy", () => {
        document.removeEventListener("keydown", onEscape);
      });
    },
  };
</script>
