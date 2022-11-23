<script>
export default {
  props: ["lists", "type", "results"],
  methods: {
    handleClear() {
      this.$emit("update:lists", []);
    },
    handleChange(e) {
      this.$emit("update:type", e.target.value);
    },
  },
};
</script>

<template>
  <div>
    <span :style="{ marginRight: '20px' }">
      {{ results["ACTIVE"].length }} item left
    </span>
    <a-radio-group :value="type" id="radioBtnGroup" :onChange="handleChange">
      <a-radio-button value="ALL">All</a-radio-button>
      <a-radio-button value="ACTIVE">Active</a-radio-button>
      <a-radio-button value="COMPLETED">Complete</a-radio-button>
    </a-radio-group>
    <a-button
      v-if="results['COMPLETED'].length"
      id="closeCompleted"
      :onClick="handleClear"
    >
      Clear Completed
    </a-button>
  </div>
</template>
<style>
#closeCompleted {
  margin-left: 20px;
}
</style>
