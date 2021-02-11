<template>
  <div class="books">
    <div v-if="books.length">
      <div v-for="book in books" :key="book.id" class="book">
        <router-link
          :to="{
            name: 'BookDetails',
            params: {
              id:
                book.title.toLowerCase().split(' ').join('-') +
                '&id=' +
                book.id,
            },
          }"
        >
          <h2>{{ book.title }}</h2>
        </router-link>
      </div>
    </div>
    <div v-else>Loading books...</div>
  </div>
</template>

<script>
export default {
  name: "Books",
  data() {
    return {
      books: [],
    };
  },
  mounted() {
    fetch("http://localhost:3000/books/")
      .then((res) => res.json())
      .then((data) => (this.books = data))
      .catch((err) => console.log(err.message));
  },
};
</script>

<style scoped>
.books a {
  text-decoration: none;
}

.books h2 {
  background: #f4f4f4;
  color: #212121;
  max-width: 400px;
  margin: 10px auto;
  padding: 20px;
  border-radius: 10px;
}

.books h2:hover {
  background: #ddd;
}
</style>