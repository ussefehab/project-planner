<template>
  <div class="project" :class="{ completed: project.complete }">
    <div class="action">
      <h3 @click="toggleDescription">{{ project.name }}</h3>
      <div class="icons">
        <router-link :to="{ name: 'EditProject', params: { id: project.id } }">
          <span class="material-icons"> edit </span>
        </router-link>
        <span class="material-icons" @click="deleteProject"> delete </span>
        <span class="material-icons tick" @click="toggleComplete"> done </span>
      </div>
    </div>
    <div class="details" v-if="showDescription">
      <p>{{ project.description }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      showDescription: false,
    };
  },
  methods: {
    toggleDescription() {
      this.showDescription = !this.showDescription;
    },
    deleteProject() {
      fetch("http://localhost:3000/projects/" + this.project.id, {
        method: "DELETE",
      }).then(() => this.$emit("delete", this.project.id));
    },
    toggleComplete() {
      fetch("http://localhost:3000/projects/" + this.project.id, {
        method: "PATCH",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({ complete: !this.project.complete }),
      }).then(() => this.$emit("update", this.project.id));
    },
  },
};
</script>

<style>
.project {
  background-color: white;
  padding: 10px 20px;
  margin: 20px auto;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.2);
  border-left: 4px solid #bb0101;
}
h3 {
  cursor: pointer;
}
.action {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.material-icons {
  font-size: 24px;
  color: #aaa;
  cursor: pointer;
}
.material-icons:hover {
  color: #333;
}
.completed {
  border-left: 4px solid #28c54c;
  text-decoration: line-through;
}
.completed .tick {
  color: #28c54c;
}
</style>
