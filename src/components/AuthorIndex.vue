<!-- AuthorIndex.vue -->
<template>
  <div class="row">
    <div style="margin-top: 5%">
      <h2>{{ title }}</h2>
      <table>
        <thead>
          <tr>
            <th>Id</th>
            <th>Author</th>
            <th>Nationality</th>
            <th>Birth Year</th>
            <th>Fields</th>
            <th class="text-center">Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(author, index) in authors" :key="index">
            <td>{{ author._id }}</td>
            <td>{{ author.author }}</td>
            <td>{{ author.nationality }}</td>
            <td>{{ author.birth_year }}</td>
            <td>{{ author.fields }}</td>
            <td>
              <router-link class="button" :to="'/author/show/' + author._id">Show</router-link>
              &nbsp;
              <router-link class="button" :to="'/author/edit/' + author._id">Edit</router-link>
              &nbsp;
              <a class="button" v-on:click="deleteAuthor(author._id)">Erase</a>
            </td>
          </tr>
        </tbody>
      </table>
      <router-link class="button button-primary" to="/author/create">New</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "AuthorIndex",
  data() {
    return {
      title: "Author List",
      authors: [],
    };
  },
  mounted() {
    this.allAuthors();
  },
  methods: {
    allAuthors() {
      fetch(this.url + '/.netlify/functions/authorFindAll', {
        headers: { Accept: 'application/json' },
      })
        .then((response) => response.json())
        .then((items) => {
          this.authors = items;
        });
    },
    deleteAuthor(id) {
      fetch(this.url + '/.netlify/functions/authorDelete/' + id, {
        headers: { 'Content-Type': 'application/json' },
        method: 'DELETE',
      }).then(() => {
        this.allAuthors();
      });
    },
  },
};
</script>
