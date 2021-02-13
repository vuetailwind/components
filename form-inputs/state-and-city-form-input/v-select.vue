<template>
  <div class="w-full md:flex justify-center">
    <div class="mb-4 px-2 w-full md:w-1/3">
      <label class="block mb-1 text-sm w-full flex justify-start" for="select-item">State:</label>

      <div class="relative">
        <select
          class="w-full border px-4 pr-8 py-2 rounded focus:border-blue-500 focus:shadow-outline outline-none appearance-none"
          id="select-item"
          v-model="form.state">
          <option disabled>select state</option>
          <option v-for="item in State" :key="item">{{ item }}</option>
        </select>

        <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700">
          <svg class="fill-current h-4 w-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20">
            <path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"/>
          </svg>
        </div>
      </div>
    </div>

    <div class="mb-4 px-2 w-full md:w-1/3">
      <label class="block mb-1 text-sm w-full flex justify-start" for="select-item">City:</label>

      <div class="relative">
        <select
          class="w-full border px-4 pr-8 py-2 rounded focus:border-blue-500 focus:shadow-outline outline-none appearance-none"
          id="select-item"
          v-model="form.city">
          <option disabled>select city</option>
          <option v-for="item in Cities[form.state]" :key="item">{{ item }}</option>
        </select>

        <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700">
          <svg class="fill-current h-4 w-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20">
            <path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"/>
          </svg>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Cities from 'components/US.json';

export default {
  data() {
    return {
      Cities,
      State: Object.keys(Cities),
      form: {
        state: "New York",
        city: "New York"
      }
    }
  }
}
</script>
