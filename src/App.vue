<template>
  <div id="app">
    <div class="container">
      <TotalBalance :total="totalBalance" />
      <!-- Pass the submitForm event handler to the FormVue component -->
      <FormVue @submitForm="onFormSubmit" />
      <BudgetList :list="list" @deleteItem="onDeleteItem" />
    </div>
  </div>
</template>

<script>
import BudgetList from "./components/BudgetList.vue";
import FormVue from "./components/Form.vue";
import TotalBalance from "./components/TotalBalance.vue";

export default {
  name: "App",
  components: {
    BudgetList,
    FormVue,
    TotalBalance,
  },
  data() {
    return {
      list: {
        1: { type: "INCOME", value: 100, comment: "Some comment", id: 1 },
        2: { type: "OUTCOME", value: -50, comment: "Outcome comment", id: 2 },
      },
    };
  },
  computed: {
    totalBalance() {
      return Object.values(this.list).reduce((acc, item) => {
        return acc + item.value;
      }, 0);
    },
  },
  methods: {
    onDeleteItem(id) {
      delete this.list[id];
    },
    // Event handler for form submission
    onFormSubmit(formData) {
      // Generate a new unique id for the task
      const id = Object.keys(this.list).length + 1;
      // Add the new task to the list
      this.list[id] = {
        type: formData.type,
        comment: formData.comment,
        value: formData.value,
        id: id,
      };
    },
  },
};
</script>

<style>
/* Your styles */
</style>
