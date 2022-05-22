<template>
  <div class="cc-card">
    <h3>{{ data.title }}</h3>
    <p>
      {{ data.description }}
    </p>
  </div>
</template>

<script>
export default {
  name: "TaskCard",
  props: ["data"],
};
</script>

<style lang="scss">
.cc-card {
  padding: 0 10px;
}
</style>
