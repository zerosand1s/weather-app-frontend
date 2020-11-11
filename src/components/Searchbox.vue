<template>
  <div class="w-full h-10 lg:h-12 flex items-center">
    <input
      class="w-full md:w-11/12 h-full px-4 py-2 text-xl rounded-lg focus:outline-none border border-gray-500 bg-white"
      type="text"
      name="search"
      v-model="query"
      v-on:keyup.enter="search"
    />
    <button
      class="w-1/5 md:w-2/12 h-full ml-4 p-2 flex justify-center items-center text-sm sm:text-lg tracking-wide leading-8 text-gray-200 focus:outline-none rounded-lg bg-gray-700 hover:bg-gray-900"
      v-on:click="search"
    >
      <!-- <img src="../assets/icons/search.svg" alt="Search" /> -->
      Search
    </button>
  </div>
</template>

<script>
export default {
  name: 'Searchbox',
  data() {
    return {
      query: ''
    };
  },
  methods: {
    search: function() {
      if (this.query.trim().length) {
        this.$emit('fetch-data', this.query);
      }
    }
  }
};
</script>
