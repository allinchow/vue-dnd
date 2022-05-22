<template>
  <div id="app" class="app-wrapper">
    <task-form @createTask="addTask"></task-form>
    <hr />
    <drag-drop
      ref="dragContainer"
      :dropzones="dropGroups"
      :dropzonesTitle="'Доска задач'"
      :originalData="stories"
      :originalTitle="'Неотсортированные задачи'"
      :inPlace="true"
      :enableSave="false"
      :enableCancel="false"
    >
      <template #dd-card="{ cardData }">
        <task-card :data="cardData" />
      </template>
    </drag-drop>
  </div>
</template>

<script>
import DragDrop from "vue-drag-n-drop";
import TaskCard from "@/components/TaskCard.vue";
import TaskForm from "@/components/TaskForm.vue";

export default {
  components: {
    DragDrop,
    TaskCard,
    TaskForm,
  },
  data() {
    return {
      componentKey: 0,
      stories: [
        {
          title: "Strategy 101",
          description: "Create a draft of business plan",
          id: 13123,
        },
        {
          title: "Strategy 102",
          description: "Finalize the plan",
          id: 2322,
        },
        {
          title: "Tech diagram",
          description: "Draw the tech data",
          id: 434234,
        },
        {
          title: "Place Holder",
          description: "Data Science Team",
          id: 34534,
        },
      ],

      dropGroups: [
        {
          name: "К выполнению",
          children: [],
        },
        {
          name: "В работе",
          children: [],
        },
        {
          name: "Готово",
          children: [],
        },
      ],
    };
  },
  created() {
    if (localStorage.getItem("stories")) {
      this.stories = JSON.parse(localStorage.getItem("stories"));
    }
  },
  methods: {
    addTask(task) {
      this.stories.push(task);
      this.saveTasksList();
    },
    saveTasksList() {
      localStorage.setItem("stories", JSON.stringify(this.stories));
    },
  },
};
</script>

<style lang="scss">
$primary: #2e6dbe;

@import url("https://fonts.googleapis.com/css2?family=PT+Sans:wght@400;700&display=swap");

.app-wrapper {
  padding: 20px;
}
body,
button,
textarea,
input {
  font-family: "PT Sans", sans-serif;
}
button {
  cursor: pointer;
}
.cc-btn {
  padding: 6px 10px 8px;
  background: $primary;
  color: #fff;
  border: 0;
  border-radius: 3px;
}
.vue-drag-n-drop {
  .dd-drop-container {
    min-height: 10em;
  }
}
</style>
