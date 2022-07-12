<template>
  <ul class="table-pagination flex justify-end bg-gray-50 text-sm space-x-3">
    <li
      class="arrow inactive block items-center w-8 h-8 border border-gray-100 rounded"
      v-if="(this.current_page !== 1)"
      @click="searchApplication(current_page-1)"
    >
      <svg xmlns="http://www.w3.org/2000/svg" class="w-3 h-3" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M12.707 5.293a1 1 0 010 1.414L9.414 10l3.293 3.293a1 1 0 01-1.414 1.414l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 0z" clip-rule="evenodd" />
      </svg>
    </li>
    <li class="arrow">
      {{ this.current_page }}
      <span class="mx-0.25">/</span>
      {{ this.last_page}}
    </li>
    <li
      class="arrow inactive block items-center w-8 h-8 border border-gray-100 rounded"
      v-if="(this.current_page !== this.last_page)"
      @click="searchBooks(current_page+1)"
    >
      <svg xmlns="http://www.w3.org/2000/svg" class="w-3 h-3" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z" clip-rule="evenodd" />
      </svg>
    </li>

  </ul>
</template>

<script>

export default {
  name: "TablePagination",
  props: {
  },
  data() {
    return {
      current_page: 1,
      last_page: "",
      range: 5,
    }
  },
  methods: {
    searchBook: async function (page) {
      const result = await searchBook({
        page: page,
        total: 20,
      });
      const books = result.books;
      const paginate = result.books;

      this.books = books;
      this.last_page = paginate.last_page;
      this.current_page = paginate.current_page;
      this.$emit("paginated-data", this.books);
    },
  },

}
</script>