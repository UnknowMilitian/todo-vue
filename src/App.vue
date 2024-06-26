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
      list: JSON.parse(localStorage.getItem("budgetItems")) || {},
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
    saveToLocalStorage() {
      localStorage.setItem("budgetItems", JSON.stringify(this.list));
    },
    onDeleteItem(id) {
      delete this.list[id];
      this.saveToLocalStorage();
    },
    onFormSubmit(formData) {
      // Generate a new unique id for the task
      const id = Object.keys(this.list).length + 1;
      // Adjust the value based on the type (INCOME or OUTCOME)
      const value =
        formData.type === "OUTCOME" ? -formData.value : formData.value;
      // Add the new task to the list
      this.list[id] = {
        type: formData.type,
        comment: formData.comment,
        value: value,
        id: id,
      };
      this.saveToLocalStorage();
    },
  },
};
</script>

<style>
/* Your styles */
</style>
