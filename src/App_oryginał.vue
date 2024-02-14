
<script setup>
import { computed, ref } from 'vue';

const books = ref([]);
const currentPage = ref(1);

const allPages = computed(() => Math.ceil(books.value.length / 100))

const booksFromPage = computed(() => books.value.slice((currentPage.value - 1) * 100, (currentPage.value - 1) * 100 + 100))

function fetchBooks() {
  fetch(`https://wolnelektury.pl/api/books`)
      .then((response) => {
        return response.json();
      })
      .then((body) => {
        books.value = body;
      })
}

function changePage(pageNum) {
  currentPage.value = pageNum;
}

function prevPage() {
  if (currentPage.value > 1) {
    currentPage.value--;
  }
}

function nextPage() {
  if (currentPage.value < allPages.value) {
    currentPage.value++;
  }
}

fetchBooks()
</script>

<template>
  <h1>Ksiazki</h1>
  <ul class="pagination">
    <li @click="prevPage">&lt;</li>
    <template v-for="pageNum in allPages" :key="pageNum">
      <li @click="changePage(pageNum)" :class="{'active': pageNum === currentPage}">&nbsp;{{ pageNum }}&nbsp;</li>
    </template>
    <li @click="nextPage">&gt;</li>
  </ul>
  <ul>
    <li v-for="(book, idx) in booksFromPage" :key="book.slug">
      <p>{{ (idx + 1) + (currentPage - 1) * 100 }}. Tytul: {{ book.title }} Autor: {{ book.author }}</p>
      <img v-bind:src="`https://wolnelektury.pl/media/${book.cover_thumb}`" />
    </li>
  </ul>
</template>

<style>
.pagination {
  list-style: none;
  display: flex;
}

.pagination li {
  cursor: pointer;
}

.pagination li:hover {
  color: #fff;
}

.pagination li.active {
  color: #fff;
  font-weight: bold;
}
</style>