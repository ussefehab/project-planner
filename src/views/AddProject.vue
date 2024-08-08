<template>
  <form @submit.prevent="handleSubmitted">
    <label>Title:</label>
    <input type="text" v-model="name" required />
    <label>description</label>
    <textarea v-model="description" required></textarea>
    <button>Add to projects</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      description: "",
    };
  },
  methods: {
    handleSubmitted() {
      let project = {
        name: this.name,
        description: this.description,
        complete: false,
      };
      fetch("http://localhost:3000/projects", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(project),
      }).then(() => this.$router.push("/"));
    },
  },
};
</script>

<style>
form {
  background: #ffffff;
  padding: 20px;
  border-radius: 10px;
}
label {
  display: block;
  color: #bbb;
  text-transform: uppercase;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 1px;
  margin: 20px 0 10px 0;
}
input {
  padding: 10px;
  border: 0;
  border-bottom: 1px solid #ddd;
  width: 100%;
  box-sizing: border-box;
}
textarea {
  border: 1px solid #ddd;
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
  height: 100px;
}
form button {
  display: block;
  margin: 20px auto 0;
  background: #00ce89;
  color: white;
  padding: 10px;
  border: 0;
  border-radius: 6px;
  font-size: 16px;
}
</style>
