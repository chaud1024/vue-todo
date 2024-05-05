<script setup>
const props = defineProps({
  item: {
    type: Object,
  },
});

const emit = defineEmits(["list-complete"]);

const listComplete = () => {
  //   console.log("list complete");
  emit("list-complete", props.item);
};
</script>

<template>
  <li
    role="listitem"
    class="todo-list"
    :class="{ complete: props.item.complete }">
    <div class="todo-list__left">
      <input
        type="checkbox"
        role="checkbox"
        aria-labelledby=""
        @click="listComplete" />
      <span id="">{{ props.item.text }}</span>
    </div>
    <div class="todo-list__right">
      <i
        class="fa-regular fa-pen-to-square"
        aria-label="편집"
        role="button"></i>
      <i class="fa-solid fa-trash-can" aria-label="삭제" role="button"></i>
    </div>
  </li>
</template>

<style scoped>
.todo-list {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 6px;

  &:hover {
    background-color: rgba(0, 128, 128, 0.161);
  }

  &.complete {
    background-color: rgba(168, 191, 191, 0.66);

    & span {
      text-decoration: line-through;
    }
  }

  .todo-list__left {
    display: flex;
    gap: 4px;
    align-items: center;
  }

  .todo-list__right {
    display: flex;
    gap: 4px;

    & i {
      cursor: pointer;
      padding: 2px 4px;

      &:hover {
        color: teal;
      }
    }
  }
}
</style>
