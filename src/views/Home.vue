<template>
  <div class="home">
    <filter-nav @filterChange="current = $event" :current="current" />
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <single-project :project="project" @delete="handleDelete" @completed="handleCompleted" />
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from '@/components/SingleProject.vue'
import FilterNav from '@/components/FilterNav.vue'

export default {
  name: 'Home',
  components: {
    SingleProject,
    FilterNav
  },
  data() {
    return {
      projects: [],
      current: 'all'
    }
  },
  mounted() {
    fetch('http://localhost:3000/projects')
      .then(res => res.json())
      .then(data => this.projects = data)
      .catch(err => console.log(err.message))
  },
  computed: {
    filteredProjects() {
      if (this.current === 'completed')
        return this.projects.filter(project => project.completed)
      if (this.current === 'ongoing')
        return this.projects.filter(project => !project.completed)
      return this.projects
      
    }
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((project) => {
        return project.id !== id
      })
    },
    handleCompleted(id) {
      let findProject = this.projects.find(project => {
        return project.id === id
      })
      findProject.completed = !findProject.completed
    }
  },
}
</script>

<style>

</style>
