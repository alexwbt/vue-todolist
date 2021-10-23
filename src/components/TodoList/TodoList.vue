<template>
  <div class="todo-list">
    <h1>Todo List</h1>
    <input
      class="todo-input"
      v-model="newTodo"
      @keydown="keydown"
      placeholder="New Todo"
    />
    <div>
      <ListItem
        v-for="(item, i) in items"
        :key="i"
        :value="item.value"
        @change="change(i)"
      />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, watch } from "vue";
import ListItem from "./ListItem.vue";

class TodoItem {
    value = '';
    checked = false;
    constructor(value: string) {
        this.value = value;
    }
}

export default defineComponent({
  components: { ListItem },
  setup() {
    const items = ref<TodoItem[]>([]);
    const newTodo = ref("");

    const keydown = (e: KeyboardEvent) => {
      if (e.key === "Enter") {
        items.value.push(new TodoItem(newTodo.value));
        newTodo.value = "";
      }
    };

    const change = (i: number) => {
        items.value[i].checked = !items.value[i].checked;
        console.log(items.value[i])
    };

    return {
      items,
      newTodo,
      keydown,
      change
    };
  },
});
</script>

<style lang="scss" scoped>
.todo-list {
  width: 800px;
  margin: auto;
  flex-direction: column;
  align-content: center;
  user-select: none;

  .todo-input {
      width: 100%;
      margin: 10px;
      padding: 10px;
      font-size: 20px;
  }

  h1 {
    text-align: center;
  }
}
</style>
