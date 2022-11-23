<script>
import { DownOutlined } from "@ant-design/icons-vue";
import FooterContent from "../components/FooterContent.vue";
import ItemContent from "../components/ItemContent.vue";

export default {
  components: {
    DownOutlined,
    "item-content": ItemContent,
    "footer-content": FooterContent,
  },
  data() {
    return {
      lists: [],
      title: "你好",
      inputValue: "",
      type: "ALL",
    };
  },
  watch: {
    // 监控
    // // 每当 question 改变时，这个函数就会执行
    // title(newQuestion, oldQuestion) {
    //   this.lists = [{ value: "oooo", edit: false, complete: false }];
    //   console.log(newQuestion, oldQuestion, "更改title了131313");
    // },
  },
  computed: {
    // 相当于react的useMemo
    handleResult() {
      return {
        ALL: this.lists,
        ACTIVE: this.lists.filter((item) => item.complete === false),
        COMPLETED: this.lists.filter((item) => item.complete === true),
      };
    },
  },
  methods: {
    onPressEnter(v) {
      this.lists.push({ value: v.target.value, complete: false, edit: false });
      this.inputValue = "";
    },
  },
};
</script>

<template>
  <main>
    <h1 class="title">TODOS</h1>
    <a-input
      class="enterInput"
      v-model:value="inputValue"
      placeholder="What needs to be done?"
      @pressEnter="onPressEnter"
    >
      <template #prefix>
        <DownOutlined />
      </template>
    </a-input>
    <!-- content -->
    <item-content
      v-model:lists="lists"
      :type="type"
      :results="this.handleResult"
    />
    <!-- footer -->
    <footer-content
      v-model:type="type"
      v-model:lists="lists"
      :results="this.handleResult"
    />
  </main>
</template>
<style>
.title {
  width: 100%;
  padding: 50px 0 30px 0;
  margin: 0;
  text-align: center;
  color: #e4aaa0;
  font-size: 70px;
}
.enterInput {
  width: 500px !important;
  font-size: 16px !important;
  padding: 12px !important;
  border: 0px !important;
  border-bottom: 2px solid #d9d9d9 !important;
  outline: none !important;
}
.enterInput .ant-input {
  margin-left: 6px;
}
.ant-input-affix-wrapper:focus,
.ant-input-affix-wrapper-focused {
  box-shadow: none !important;
  outline: none !important;
}
</style>
