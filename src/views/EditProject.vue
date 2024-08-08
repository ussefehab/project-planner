<template>
  <h1>Edit project</h1>
  <form @submit.prevent="editHandler">
    <label>Title:</label>
    <input type="text" v-model="name" required />
    <label>description</label>
    <textarea v-model="description" required></textarea>
    <button>Edit project</button>
  </form>
</template>

<script>
export default {
  props: ["id"],
  data() {
    return {
      name: "",
      description: "",
      uri: "http://localhost:3000/projects/" + this.id,
    };
  },
  mounted() {
    fetch(this.uri)
      .then((res) => res.json())
      .then((data) => {
        this.name = data.name;
        this.description = data.description;
      });
  },
  methods: {
    editHandler() {
      fetch(this.uri, {
        method: "PATCH",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          name: this.name,
          description: this.description,
        }),
      }).then(() => this.$router.push("/"));
    },
  },
};
</script>

<style></style>
