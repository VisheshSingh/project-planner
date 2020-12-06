<template>
  <FilterNav :current="current" @filterChange="current = $event" />
  <div v-if="projects.length">
    <div v-for="project in filteredProjects" :key="project.id">
      <SingleProject
        :project="project"
        @delete="handleDelete"
        @complete="handleDone"
      />
    </div>
  </div>
</template>

<script>
import SingleProject from '../components/SingleProject.vue';
import FilterNav from '../components/FilterNav.vue';

export default {
  name: 'Home',
  components: { SingleProject, FilterNav },
  data() {
    return {
      projects: [],
      current: 'all',
    };
  },
  mounted() {
    const fetchProjects = async () => {
      const res = await fetch('http://localhost:3000/projects');
      const data = await res.json();
      this.projects = data;
    };
    fetchProjects();
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((project) => project.id !== id);
    },
    handleDone(id) {
      const p = this.projects.find((project) => project.id === id);
      p.complete = !p.complete;
    },
  },
  computed: {
    filteredProjects() {
      if (this.current === 'completed') {
        return this.projects.filter((project) => project.complete);
      } else if (this.current === 'ongoing') {
        return this.projects.filter((project) => !project.complete);
      } else {
        return this.projects;
      }
    },
  },
};
</script>
