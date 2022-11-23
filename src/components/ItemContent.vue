<!-- eslint-disable vue/no-mutating-props -->
<script>
import { CloseOutlined, CheckCircleOutlined } from "@ant-design/icons-vue";

export default {
  props: ["lists", "type", "results"],
  components: {
    CloseOutlined,
    CheckCircleOutlined,
  },
  methods: {
    handleDelete(index) {
      this.lists.splice(index, 1);
      this.$emit("update:lists", this.lists);
    },
    handleComplete(e, index, type) {
      e.stopPropagation();
      let result = this.lists.map((v, i) => {
        if (i === index) {
          return type ? { ...v, complete: true } : { ...v, complete: false };
        }
        return v;
      });
      this.$emit("update:lists", result);
    },
    handleEdit(e, index) {
      e.stopPropagation();
      let result = this.lists.map((v, i) => {
        if (i === index) {
          return { ...v, edit: true };
        }
        return v;
      });
      this.$emit("update:lists", result);
    },
    handleCloseEdit(e, index) {
      e.stopPropagation();
      let result = this.lists.map((v, i) => {
        if (i === index) {
          return { ...v, value: e.target.value, edit: false };
        }
        return v;
      });
      this.$emit("update:lists", result);
    },
  },
};
</script>

<template>
  <div v-for="(v, index) in results[type]" :key="index">
    <div class="listContent">
      <a-input
        id="editInput"
        v-if="v.edit"
        v-model:value="v.value"
        @pressEnter="(e) => handleCloseEdit(e, index)"
      />
      <div
        v-if="!v.edit"
        class="circleContent"
        :onClick="(e) => handleEdit(e, index)"
      >
        <CheckCircleOutlined
          v-if="v.complete"
          id="checkBtn"
          :onClick="(e) => handleComplete(e, index)"
        />
        <span
          v-if="!v.complete"
          class="circle"
          :onClick="(e) => handleComplete(e, index, 'open')"
        ></span>
        <span
          class="content"
          :style="{ color: v.complete ? '#d9d9d9' : '#595959' }"
        >
          {{ v?.value || "" }}
          <span v-if="v.complete" class="completed"></span>
        </span>
      </div>
      <CloseOutlined
        v-if="!v.edit"
        id="closeBtn"
        :onClick="() => handleDelete(index)"
      />
    </div>
  </div>
</template>
<style>
.listContent {
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-bottom: 1px solid #f2f2f2;
  height: 54px;
  cursor: pointer;
}
.circleContent {
  display: flex;
  align-items: center;
}

.completed {
  display: flow-root;
  border: 1px solid#d9d9d9;
  position: relative;
  top: -12px;
}
#checkBtn {
  color: green;
  width: 30px;
  height: 30px;
  font-size: 30px;
  cursor: pointer;
}
.circle {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  background: #fff;
  border: 1px solid #d9d9d9;
  cursor: pointer;
}
.content {
  font-size: 16px;
  margin-left: 12px;
  color: #595959;
}
#closeBtn {
  color: #a45f60;
  font-size: 16px;
  font-weight: bolder;
  cursor: pointer;
}
#editInput {
  border: 0;
  margin-left: 20px;
  width: 96%;
  font-size: 16px;
  padding: 7px 11px;
  outline: none;
}
#radioBtnGroup {
  margin-top: 30px;
}
#closeCompleted {
  margin-left: 20px;
}
</style>
