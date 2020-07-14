<template>
  <div class="inline-flex">
    <div class="select-none border py-2 px-4 cursor-pointer bg-gray-100 hover:bg-gray-200 rounded-l"
         @click="decrease">
      -
    </div>

    <input class="border p-2 text-center outline-none" type="text" v-model="number" :name="name">

    <div class="select-none border py-2 px-4 cursor-pointer bg-gray-100 hover:bg-gray-200 rounded-r"
         @click="increase">
      +
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        number: 1
      }
    },
    props: {
      name: {
        type: String,
        required: true
      }
    },
    methods: {
      increase() {
        this.number++;
      },
      decrease() {
        if (this.number > 1) {
          this.number--;
        }
      },
    }
  };
</script>
