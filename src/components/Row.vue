<template>
  <div class="row">
    <button @click="repeat">Rep</button>
    <span class="row-text">
      R{{index}} -
      <input type="text" :value="value" @input="change">
    </span>
    <button @click="del">Del</button>
  </div>
</template>

<script>
export default {
  name: "Row",
  props: {
    value: String,
    index: Number
  },
  methods: {
    repeat() {
      this.$emit("repeat", this.index);
    },
    del() {
      this.$emit("del", this.index - 1);
    },
    change(input) {
      this.$emit("change", input.target.value, this.index - 1);
    }
  }
};
</script>
<style scoped>
.row {
  align-content: flex-start;
  text-align: left;
  margin-bottom: 5px;
}
.row-text {
  margin-left: 15px;
  margin-right: 15px;
}
</style>

