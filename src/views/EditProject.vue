<template>
  <form @submit.prevent="handleSubmit" class="edit-project">
    <h4>Edit Project</h4>
    <label for="title">Title:</label>
    <input type="text" id="title" v-model="title" />
    <label for="details">Details:</label>
    <textarea id="details" v-model="details" />
    <input type="checkbox" v-model="complete" />
    <label for="complete" class="completed">Completed</label>
    <div class="submit">
      <button type="submit">Save</button>
    </div>
  </form>
</template>

<script>
export default {
  name: 'EditProject',
  props: ['id'],
  data() {
    return {
      title: '',
      details: '',
      complete: null,
    };
  },
  mounted() {
    fetch(`http://localhost:3000/projects/${this.id}`)
      .then((res) => res.json())
      .then((data) => {
        this.title = data.title;
        this.details = data.details;
        this.complete = data.complete;
      })
      .catch((err) => console.log(err.message));
  },
  methods: {
    handleSubmit() {
      const project = {
        title: this.title,
        details: this.details,
        complete: this.complete,
      };
      fetch(`http://localhost:3000/projects/${this.id}`, {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(project),
      })
        .then(() => this.$router.push('/'))
        .catch((err) => console.log(err.message));
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
h4 {
  color: #aaa;
  text-align: center;
  text-transform: uppercase;
  font-weight: normal;
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
  height: 100px;
}
input[type='checkbox'] {
  display: inline-block;
  width: 5%;
}
label.completed {
  display: inline-block;
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
