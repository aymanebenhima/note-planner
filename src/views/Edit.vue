<template>
  <div class="edit">
      <h3>Edit project</h3>
    <form @submit.prevent="editProject">
      <label for="title">Title:</label>
      <input type="text" v-model="title" name="title" required>
      <label for="details">Details:</label>
      <textarea v-model="details" name="details" required></textarea>
      <button>Update</button>
    </form>
  </div>
</template>

<script>
export default {
    props: ['id'],
    data() {
        return {
            title: '',
            details: '',
            uri: `http://localhost:3000/projects/${this.id}`
        }
    },
    mounted() {
        fetch(this.uri)
            .then(res => res.json())
            .then(data => {
                this.title = data.title
                this.details = data.details
                })
            .catch(err => console.log(err))
    },
    methods: {
        editProject() {
            fetch(this.uri, {
                method: 'PATCH',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({
                    title: this.title,
                    details: this.details
                })
            }).then(() => {
                this.$router.push('/')
            }).catch(err => console.log(err))
        }
    },
}
</script>

<style>

</style>