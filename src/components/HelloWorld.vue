<template>
  <div class="wrapper">
    <div class="input-wrapper">
      <button @click="copy">Copy</button>
      <input type="text" v-model="newRow">
      <button @click="addRow">add row</button>
    </div>
    <div class="list">
      <Row
        @repeat="repeat"
        @del="del"
        v-for="(row, index) in rows"
        :key="index"
        :index="index+1"
        :value="row"
        @change="change"
      ></Row>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import Clipboard from "v-clipboard";
Vue.use(Clipboard);
import Row from "./Row";
export default {
  name: "HelloWorld",
  props: {
    msg: String
  },
  data() {
    return {
      rows: [],
      newRow: ""
    };
  },
  methods: {
    addRow() {
      this.rows.push(this.newRow);
      this.newRow = "";
    },
    repeat(index) {
      this.rows.push("rep R" + index);
    },
    copy() {
      this.$clipboard(this.textCopy);
    },
    del(index) {
      this.rows.splice(index, 1);
    },
    change(text, index) {
      this.rows.splice(index, 1, text);
    }
  },
  computed: {
    textCopy() {
      var string = "";
      this.rows.forEach((row, index) => {
        var rowNumber = index + 1;
        string = string + "R" + rowNumber + " - " + row + "\n";
      });
      return string;
    }
  },
  components: {
    Row
  }
};
</script>

<style scoped>
.wrapper {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}

.input-wrapper {
  display: flex;
  flex-direction: column;
  width: fit-content;
}

.list {
  display: flex;
  flex-direction: column;
  width: fit-content;
}
</style>

