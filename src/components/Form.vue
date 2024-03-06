<template>
  <div id="form">
    <div class="card form-card" lable-position="top">
      <form action="" class="field" ref="addItemForm" :model="formData">
        <label class="label">Subject</label>
        <div class="control">
          <div class="select">
            <select v-model="formData.type">
              <option>INCOME</option>
              <option>OUTCOME</option>
            </select>
          </div>
        </div>

        <label class="label mt-3">Comment</label>
        <div class="control">
          <input
            class="input"
            v-model="formData.comment"
            type="text"
            placeholder="Comment"
          />
        </div>

        <label class="label mt-3">Value</label>
        <div class="control">
          <input
            class="input"
            v-model.number="formData.value"
            type="number"
            placeholder="Value"
          />
        </div>

        <button @click="onSubmit" class="button btn-form is-success mt-5">
          Submit
        </button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "FormVue",
  data() {
    return {
      formData: {
        type: "INCOME",
        comment: "",
        value: 0,
      },
      formErrors: {},
    };
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();
      // Emit an event to the parent component with the form data
      this.$emit("submitForm", { ...this.formData });
      // Reset the form
      this.resetForm();
    },
    resetForm() {
      // Reset form data
      this.formData = {
        type: "INCOME",
        comment: "",
        value: 0,
      };
    },
  },
};
</script>

<style scoped>
#form {
  width: 600px;
  margin: 0 auto;
}

#form form {
  padding: 1.25rem;
}

#form form .select,
#form form .select select {
  width: 100%;
}

button.btn-form {
  margin: 0 auto;
  display: block;
}
</style>
