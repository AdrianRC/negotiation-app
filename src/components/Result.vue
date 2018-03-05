<template>
  <div id="result">
    <h1>{{ outcome }}</h1>
    <p>The employer's maximum offer was: ${{ employer }}</p>
    <p>While the employee's minimum expected salary was: ${{ employee }}</p>
  </div>
</template>

<script>
export default {
  //prop validation.
  props: {
    employer: {
      type: Number,
      required: true
    },
    employee: {
      type: Number,
      required: true
    }
  },
  computed: {
    outcome() {
      return this.employer >= this.employee ? "Success!" : "Failure";
    }
  }
};
</script>

