<template>
  <div class="book" v-if="book">
    <img :src="require(`../../assets/${book.imageLink}`)" />
    <h2>Author: {{ book.author }}</h2>
    <h3>Year: {{ book.year }}</h3>
    <h3>Pages: {{ book.pages }}</h3>
    <h3>Country: {{ book.country }}</h3>
    <h3>Language: {{ book.language }}</h3>

    <a :href="book.link" target="_blank">👉 For more info click here 👈</a>
  </div>
  <div v-else>
    <p>Loading book details...</p>
  </div>
</template>

<script>
export default {
  props: ["id"],
  data() {
    return {
      book: null,
    };
  },
  mounted() {
    fetch("http://localhost:3000/books/" + this.id.split("&id=")[1])
      .then((res) => res.json())
      .then((data) => (this.book = data))
      .catch((err) => console.log(err.message));
  },
};
</script>

<style scoped>
.book {
  background: #ff5622be;
  max-width: 500px;
  margin: 20px auto;
  color: #fff;
  padding: 20px;
  border-radius: 20px;
  border: 3px solid #3f51b5be;
}

.book a {
  font-weight: 700;
  text-decoration: none;
  color: #fff;
}
</style>