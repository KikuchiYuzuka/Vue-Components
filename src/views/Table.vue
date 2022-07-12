<template>
<div class="container">
  <div class="application-table relative overflow-x-auto sm:rounded-lg">
    <table class="w-full text-left">
      <thead class="text-xs text-gray-600 bg-gray-50">
        <tr>
          <th v-for="(header, index) in headers" :key="index" class="title">
            <p @click="sortBy(header.value)" :class="addClass(header.value)">
              {{ header.text }}
            </p>
          </th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="book in sort_books" class="text-sm hover:bg-gray-50">
          <td class="column center">
            {{ book.text }}
          </td>
        </tr>
      </tbody>
    </table>
        <table-pagination @paginated-data='PaginatedData'></table-pagination>
  </div>
</div>
</template>

<script>
import TablePagination from "@/components/TablePagination.vue";

export default {
  name: "BooksTable",
  props: {
    // books: { 本来は　サーバーから渡したい
    //   type: Array,
    //   required: false
    // },
  },
  data() {
    return {
      headers: [
        {
          text: '番号',
          value: 'number',
        },
        {
          text: 'カテゴリー',
          value: 'category',
        },
        {
          text: 'タイトル',
          value: 'title'
        },
        {
          text: '作者',
          value: 'writer'
        },
        {
          text: '購入日',
          value: 'bought_date'
        },
        {
          text: 'DL',
          value: ''
        },
      ],
     // 仮で表示させるために宣言
      books: [
        {
          text: '番号',
          value: '1',
        },
        {
          text: 'カテゴリー',
          value: 'サスペンス',
        },
        {
          text: 'タイトル',
          value: 'そして誰もいなくなった'
        },
        {
          text: '作者',
          value: 'アガサ・クリスティー'
        },
        {
          text: '購入日',
          value: '2022/07/01'
        },
      ],
      sort_key: "",
      sort_asc: true,
      books: this.books,
    }
  },
  methods: {
    sortBy(key) {
      this.sort_key === key
        ? (this.sort_asc = !this.sort_asc)
        : (this.sort_asc = true);
      this.sort_key = key;
    },
    addClass(key) {
      return {
        asc: this.sort_key === key && this.sort_asc,
        desc: this.sort_key === key && !this.sort_asc,
      };
    },
    PaginatedData(value) {
      this.books = value;
    },
  },
  computed: {
    sort_books() {
      if (this.sort_key !== "") {
        let set = 1;
        this.sort_asc ? (set = 1) : (set = -1);
        this.books.sort((a, b) => {
          if (a[this.sort_key] < b[this.sort_key]) return -1 * set;
          if (a[this.sort_key] > b[this.sort_key]) return set;
          return 0;
        });
        return this.books;
      } else {
        return this.books;
      }
    },
  },
}
</script>