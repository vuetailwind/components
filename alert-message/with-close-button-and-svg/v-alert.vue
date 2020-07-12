<template>
  <div class="mb-4 border-l-4 rounded px-4 py-3" v-if="show"
       :class="wrapperColor"
       role="alert">
    <div class="flex items-start">
      <div class="py-1">
        <svg class="fill-current h-6 w-6 mr-4" :class="svgColor"
             xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20">
          <path v-if="type === 'info'"
                d="M2.93 17.07A10 10 0 1 1 17.07 2.93 10 10 0 0 1 2.93 17.07zm12.73-1.41A8 8 0 1 0 4.34 4.34a8 8 0 0 0 11.32 11.32zM9 11V9h2v6H9v-4zm0-6h2v2H9V5z"/>
          <path v-if="type === 'warning'"
                d="M2.93 17.07A10 10 0 1 1 17.07 2.93 10 10 0 0 1 2.93 17.07zm12.73-1.41A8 8 0 1 0 4.34 4.34a8 8 0 0 0 11.32 11.32zM9 5h2v6H9V5zm0 8h2v2H9v-2z"/>
          <path v-if="type === 'success'"
                d="M2.93 17.07A10 10 0 1 1 17.07 2.93 10 10 0 0 1 2.93 17.07zm12.73-1.41A8 8 0 1 0 4.34 4.34a8 8 0 0 0 11.32 11.32zM6.7 9.29L9 11.6l4.3-4.3 1.4 1.42L9 14.4l-3.7-3.7 1.4-1.42z"/>
          <path v-if="type === 'danger'"
                d="M2.93 17.07A10 10 0 1 1 17.07 2.93 10 10 0 0 1 2.93 17.07zm12.73-1.41A8 8 0 1 0 4.34 4.34a8 8 0 0 0 11.32 11.32zM6.7 9.29L9 11.6l4.3-4.3 1.4 1.42L9 14.4l-3.7-3.7 1.4-1.42z"/>
        </svg>
      </div>

      <div>
        <p class="text-sm">
          <slot></slot>
        </p>
      </div>

      <div class="flex-1 flex justify-end items-center">
        <div class="cursor-pointer" @click="show = false">
          <svg class="fill-current h-4 w-4 ml-4" :class="svgColor + ' hover:' + wrapperColor"
               xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20">
            <path
              d="M10 8.586L2.929 1.515 1.515 2.929 8.586 10l-7.071 7.071 1.414 1.414L10 11.414l7.071 7.071 1.414-1.414L11.414 10l7.071-7.071-1.414-1.414L10 8.586z"/>
          </svg>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        show: true
      }
    },
    computed: {
      shade() {
        switch (this.type) {
          case 'info':
            return 'gray';
          case 'warning':
            return 'yellow';
          case 'success':
            return 'teal'
          case 'danger':
            return 'red';
        }
      },
      wrapperColor() {
        return `bg-${this.shade}-100 text-${this.shade}-900 border-${this.shade}-500`;
      },
      svgColor() {
        return `text-${this.shade}-500`;
      }
    },
    props: {
      type: {
        type: String,
        default: 'info',
        validator: (value) => ['info', 'warning', 'success', 'danger'].indexOf(value) !== -1,
      },
    }
  }
</script>
