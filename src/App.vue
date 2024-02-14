<script setup>
import { computed, ref } from 'vue'

const books = ref([])
const currentPage = ref(1)
const allPages = computed(() => Math.ceil(books.value.length / 100))
const visiblePages = computed(() => {
  const startPage = Math.max(1, currentPage.value - 5)
  const endPage = Math.min(allPages.value, currentPage.value + 5)
  return Array.from(Array(endPage - startPage + 1), (_, i) => startPage + i)
})

const booksFromPage = computed(() =>
  books.value.slice((currentPage.value - 1) * 100, (currentPage.value - 1) * 100 + 99)
)

function fetchBooks() {
  fetch(`https://wolnelektury.pl/api/books`)
    .then((response) => {
      return response.json()
    })
    .then((body) => {
      books.value = body
    })
}

function changePage(pageNum) {
  currentPage.value = pageNum
}

function prevPage() {
  if (currentPage.value > 1) {
    currentPage.value--
  }
}

function nextPage() {
  if (currentPage.value < allPages.value) {
    currentPage.value++
  }
}

fetchBooks()
</script>

<template>
  <div class="container">
    <h1>Najlepszy katalog Ksiażek ever</h1>
    <div class="pagination">
      <span @click="prevPage">&lt;&lt;&lt;</span>
      <template v-for="pageNum in visiblePages" :key="pageNum">
        <p @click="changePage(pageNum)" :class="{ active: pageNum === currentPage }">
          &nbsp;{{ pageNum }}&nbsp;
        </p>
      </template>
      <span @click="nextPage">&gt;&gt;&gt;</span>
    </div>

    <div class="grid">
      <div v-for="(book, idx) in booksFromPage" :key="book.slug">
        <div class="book-item">
          <h4>{{ idx + 1 + (currentPage - 1) * 100 }}</h4>
          <h3>{{ book.title }}</h3>
          <h4>{{ book.author }}</h4>
          <h5 class="genre">{{ book.genre }}</h5>
          <img v-bind:src="`https://wolnelektury.pl/media/${book.cover_thumb}`" />
          <img v-if="book.has_audio" src="./components/icons/headphone.png" />
          <img v-else src="./components/icons/headphoneno.png" />
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.container {
  margin: 0 auto;
  max-width: 1200px;
}
.pagination {
  list-style: none;
  display: flex;
  justify-content: center;
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
  margin: 0 auto;
}
.grid {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  gap: 30px;
}
.book-item {
  margin: 0 auto;
}
.genre {
  color: blue;
}
</style>
