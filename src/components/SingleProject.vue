<template>
  <div class="project" :class="{ completed: project.completed }">
    <div class="actions">
      <h3 @click="showDetails = !showDetails">{{ project.title }}</h3>
      <div class="icons">
          <router-link :to="{ name: 'Edit', params: {id: project.id} }">
            <span class="material-icons">edit</span>
          </router-link>
        <span @click="deleteProject" class="material-icons">delete</span>
        <span @click="completedProject" class="material-icons tick">done</span>
      </div>
    </div>
    <div class="details" v-if="showDetails">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      showDetails: false,
      uri: `http://localhost:3000/projects/${this.project.id}`,
    };
  },
  methods: {
    deleteProject() {
      fetch(this.uri, { method: "DELETE" })
        .then(() => this.$emit("delete", this.project.id))
        .catch((err) => console.log(err.message));
    },
    completedProject() {
      fetch(this.uri, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ completed: !this.project.completed }),
      })
        .then(() => this.$emit("completed", this.project.id))
        .catch((err) => console.log(err.message));
    },
  },
};
</script>

<style>
.project {
  margin: 20px auto;
  background: white;
  padding: 10px 20px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
  border-left: 4px solid #e90074;
}
h3 {
  cursor: pointer;
}
.actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.material-icons {
  font-size: 1.5em;
  margin-left: 10px;
  color: #bdc3c7;
  cursor: pointer;
}
.material-icons:hover {
  color: #7f8c8d;
}
.project.completed {
  border-left: 4px solid #2ecc71;
}
.project.completed .tick {
    color: #2ecc71;
}
</style>
