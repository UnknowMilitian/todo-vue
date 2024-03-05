<template>
  <div id="app">
    <div class="container">
      <TotalBalance :total="totalBalance" />
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
        acc + item.value;
      }, 0);
    },
  },
  methods: {
    onDeleteItem(id) {
      delete this.list[id];
    },
    onFormSubmit(data) {
      console.log(data);
    },
  },
};
</script>

<style>
/* Component-specific styles can go here */
</style>
