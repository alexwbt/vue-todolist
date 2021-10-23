<template>
  <div class="todo-list-item">
    <label>
      <input
        type="checkbox"
        :checked="checked"
        @change="$emit('change')"
      />
      <span v-if="!checked">{{ value }}</span>
      <s v-if="checked">{{ value }}</s>
    </label>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    value: String,
    checked: Boolean,
  },
});
</script>

<style lang="scss" scoped>
.todo-list-item {
  display: block;
  text-align: left;
  background-color: white;
  padding: 5px;

  :hover {
    cursor: pointer;
  }

  label {
    display: inline-block;
  }

  span,
  s {
    display: inline-block;
    padding: 5px;
    font-size: 30px;
  }
}
</style>
