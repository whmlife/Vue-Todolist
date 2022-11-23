<script>
export default {
  props: {
    title: { type: String },
  },
  mounted() {},
  methods: {
    btnClick() {
      this.$emit("update:title", this.title + "美美美美美美美");
    },
  },
};
</script>

<template>
  <div>{{ title }}</div>
  <button @click="btnClick">改变title</button>
</template>
