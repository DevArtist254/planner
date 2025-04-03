<template>
  <div class="home">
    <div v-if="projects.length">
      <div :key="project.id" v-for="project in projects">
        <SingleProject :project="project" @delete="handleDelete" @updateComplete="handleComplete" />
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from '@/components/SingleProject.vue';



export default {
  name: 'HomeView',
  components: {
    SingleProject
  },
  data() {
    return {
      projects: []
    }
  },
  mounted() {
    fetch('http://localhost:3000/projects')
      .then(res => res.json())
      .then(data => this.projects = data)
      .catch(err => console.log(err.message))
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((p) => p.id !== id)
    },
    handleComplete(id) {
      let p = this.projects.find(p => p.id === id);

      p.complete = !p.complete
    }
  }
}
</script>
