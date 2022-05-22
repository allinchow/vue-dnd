<template>
  <div class="form-wrapper">
    <h2>Добавить задачу</h2>
    <form @submit.prevent="createTask">
      <input type="text" v-model="form.title" required placeholder="Название" />
      <textarea v-model="form.description" placeholder="Описание"></textarea>
      <button type="submit" class="cc-btn">Добавить</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "TaskForm",
  data() {
    return {
      form: this.setInittialState(),
      btnDisabled: true,
    };
  },
  methods: {
    setInittialState() {
      return {
        title: "",
        description: "",
        id: "",
      };
    },
    createTask() {
      if (!this.form.title) return;

      this.$emit("createTask", {
        title: this.form.title,
        description: this.form.description,
        id: Date.now(),
      });
      this.form = this.setInittialState();
    },
  },
};
</script>

<style lang="scss">
form {
  margin-bottom: 30px;
}
input,
textarea {
  display: block;
  width: 100%;
  max-width: 300px;
  margin: 10px 0;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 3px;
}
</style>
