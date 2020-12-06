<template>
  <div v-if="projects.length">
    <div v-for="project in projects" :key="project.id">
      <h2>{{ project.title }}</h2>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home',
  components: {},
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
};
</script>
