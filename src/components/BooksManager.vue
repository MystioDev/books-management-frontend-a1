<script setup>
import { getBooks, createBook } from "../api/books";
</script>

<script>
export default {
  name: "BooksManager",
  data() {
    return {
      books: [],
      newBook: {
        title: "",
        author: "",
        year: 2000,
      },
    };
  },
  methods: {
    async loadBooks() {
      this.books = await getBooks();
    },
    async addBook(book) {
      await createBook(book);
      await this.loadBooks();
    },
    async submitCreateBook() {
      await this.addBook(this.newBook);
    },
  },
  mounted() {
    this.loadBooks();
  },
};
</script>

<template>
  <main class="flex justify-center items-center flex-col">
    <h1 class="">Könyvtár kezelőfelület</h1>

    <form
      @submit.prevent="submitCreateBook"
      class="w-full my-10 border-2 border-stone-200 p-3 flex flex-col gap-2 rounded-xl"
    >
      <div class="flex flex-col">
        <label for="title" class="">Könyv cím:</label>
        <input
          v-model="newBook.title"
          type="text"
          name="title"
          id=""
          class="border-2 border-stone-200 rounded-lg py-1 px-2"
        />
      </div>

      <div class="flex flex-col">
        <label for="author" class="">Könyv szerzője:</label>
        <input
          v-model="newBook.author"
          type="text"
          name="author"
          id=""
          class="border-2 border-stone-200 rounded-lg py-1 px-2"
        />
      </div>

      <div class="flex flex-col">
        <label for="year" class="">Könyv megjelenésének éve:</label>
        <input
          v-model="newBook.year"
          type="number"
          name="year"
          id=""
          class="border-2 border-stone-200 rounded-lg py-1 px-2"
        />
      </div>

      <button
        type="submit"
        class="border-2 border-stone-200 rounded-lg p-2 mt-4"
      >
        Létreozás
      </button>
    </form>

    <table class="">
      <thead class="">
        <tr class="">
          <th class="">azonosító</th>
          <th class="">címe</th>
          <th class="">szerző</th>
          <th class="">megjelenése éve</th>
          <th class="">műveletek</th>
        </tr>
      </thead>
      <tbody class="">
        <tr v-for="book in books" :key="book.id" class="">
          <td class="">{{ book.id }}</td>
          <td class="">{{ book.title }}</td>
          <td class="">{{ book.author }}</td>
          <td class="">{{ book.year }}</td>
          <td class="">-</td>
        </tr>
      </tbody>
    </table>
  </main>
</template>
