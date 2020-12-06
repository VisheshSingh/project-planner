<template>
  <form @submit.prevent="handleSubmit" class="add-project">
    <label for="title">Title:</label>
    <input type="text" id="title" v-model="title" />
    <label for="details">Details:</label>
    <textarea id="details" v-model="details" />
    <div class="submit">
      <button type="submit">Add Project</button>
    </div>
  </form>
</template>

<script>
export default {
  name: 'AddProject',
  data() {
    return {
      title: '',
      details: '',
    };
  },
  methods: {
    handleSubmit() {
      const project = {
        title: this.title,
        details: this.details,
        complete: false,
      };
      console.log(project);
    },
  },
};
</script>

<style>
form {
  background: #fff;
  padding: 20px;
  border-radius: 10px;
  margin: 40px auto;
}
label {
  display: block;
  margin: 20px 0 10px 0;
  color: #bbb;
  text-transform: uppercase;
  letter-spacing: 1px;
}
input {
  padding: 10px;
  width: 100%;
  border: none;
  box-sizing: border-box;
  border-bottom: 1px solid #ddd;
}
textarea {
  padding: 10px;
  width: 100%;
  border: 1px solid #ddd;
  box-sizing: border-box;
}
.submit {
  text-align: center;
}
button {
  background: #00ce89;
  color: #fff;
  border-radius: 4px;
  padding: 10px 20px;
  border: none;
  margin: 20px auto;
}
</style>
