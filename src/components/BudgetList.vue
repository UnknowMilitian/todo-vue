<template>
  <div id="budget-list">
    <div class="budget budget-list-wrap">
      <div class="card">
        <header class="card-header has-text-centered">
          <p class="card-header-title title is-4 block">{{ header }}</p>
        </header>
      </div>
      <template v-if="!isEmpty">
        <ul>
          <li class="card bg-budget" v-for="(item, prop) in list" :key="prop">
            <div class="content">
              <span class="budget-comment">{{ item.comment }} </span>
              <span class="budget-value">{{ item.value }} </span>
              <button class="button is-danger" @click="deleteItem(item.id)">
                Delete
              </button>
            </div>
          </li>
        </ul>
      </template>
      <p class="is-empty title is-4" v-else>{{ emptyTitle }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "BudgetList",
  props: { list: { type: Object, default: () => ({}) } },
  data() {
    return {
      header: "Budget List",
      emptyTitle: "Empty List",
    };
  },
  methods: {
    deleteItem(id) {
      this.$emit("deleteItem", id);
    },
  },
  computed: {
    isEmpty() {
      return !Boolean(Object.keys(this.list).length);
    },
  },
};
</script>

<style scoped>
.budget-list-wrap {
  width: 600px;
  margin: 2rem auto;
}

.bg-budget {
  margin: 1rem 0;
  background: white;
  padding: 1.4rem;
  border-radius: 0.3rem;
}

.bg-budget .content {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

p {
  text-align: center;
  display: block;
}

p.is-empty {
  margin: 2rem 0 0 0;
  color: crimson;
}
</style>
