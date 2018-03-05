<template>
  <div id="Employee">
      <label for="salary">Please enter your minimum expected salary: $</label>
      <input type="number" id="salary" v-model="salary" v-if="!disabled"><span v-if="disabled">{{ salary }}</span>
      <button class="submit" :disabled="disabled" @click="handleSubmit">Submit</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      salary: 1,
      disabled: false
    };
  },
  methods: {
    //emits an event after the submit button is clicked.
    handleSubmit() {
      this.$emit("salarySelected", {
        author: "employee",
        value: Number.parseFloat(this.salary)
      });
      this.disabled = true;
    }
  }
};
</script>

