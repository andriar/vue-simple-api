<template>
  <div id="app">
    <table>
      <tr>
        <th>Id</th>
        <th>Title</th>
        <th>Body</th>
      </tr>
      <tr v-for="(result, index) in results" :key="index">
        <td>{{ result.id }}</td>
        <td>{{ result.title }}</td>
        <td>{{ result.body }}</td>
      </tr>
    </table>

    <div>
      <input type="text" v-model="title" />
      <input type="text" v-model="body" />
      <button @click="postData">save</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},

  data() {
    return {
      results: [],
      title: "",
      body: "",
    };
  },
  methods: {
    async getData() {
      const data = await fetch(
        "https://jsonplaceholder.typicode.com/posts/101"
      );
      const res = await data.json();

      console.info(res);
      console.info(this.results);
      this.results = res.filter((el) => el.id <= 103);
    },
    async postData() {
      const katalog = {
        title: this.title,
        body: this.body,
      };
      console.info(this.title, " ", this.body);
      let response = await fetch("https://jsonplaceholder.typicode.com/posts", {
        method: "POST",
        headers: {
          "Content-Type": "application/json;charset=utf-8",
        },
        body: JSON.stringify(katalog),
      });
      let result = await response.json();
      alert(result.message);
    },
  },
  mounted() {
    this.getData();
  },
  created() {
    console.info("");
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

td,
th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}
</style>
