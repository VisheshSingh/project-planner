<template>
  <div v-if="projects.length">
    <div v-for="project in projects" :key="project.id">
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

export default {
  name: 'Home',
  components: { SingleProject },
  data() {
    return {
      projects: [],
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
};
</script>
