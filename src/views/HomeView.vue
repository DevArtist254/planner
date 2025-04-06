<template>
  <div class="home">
    <FilterNav @filterChange="current = $event" :current="current" @click="filterProjects" />
    <div v-if="projects.length">
      <div :key="project.id" v-for="project in filteredProjects">
        <SingleProject :project="project" @delete="handleDelete" @updateComplete="handleComplete" />
      </div>
    </div>
  </div>
</template>

<script>
import FilterNav from '@/components/FilterNav.vue';
import SingleProject from '@/components/SingleProject.vue';

export default {
  name: 'HomeView',
  components: {
    SingleProject, FilterNav
  },
  data() {
    return {
      projects: [],
      filteredProjects: [],
      current: 'all'
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
  },
  computed: {
    filterProjects() {
      if (this.current === 'all') this.filteredProjects = this.projects;
      if (this.current === 'completed') this.filteredProjects = this.projects.filter(el => el.complete === true);
      if (this.current === 'ongoing') this.filteredProjects = this.projects.filter(el => el.complete === false);
    }
  }
}
</script>
