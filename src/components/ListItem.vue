<script setup>
import { nextTick, ref } from "vue";
const props = defineProps({
  item: {
    type: Object,
  },
});

const copyPropsItem = ref(props.item);

const emit = defineEmits(["list-complete", "list-delete", "list-update"]);

const inputRef = ref(null);
const editMode = ref(false);

const listComplete = () => {
  //   console.log("list complete");
  emit("list-complete", props.item);
};

const listDelete = () => {
  emit("list-delete", props.item);
};

const editModeChange = () => {
  editMode.value = !editMode.value;
  nextTick(() => {
    // nextTick : 데이터 변경 후 DOM이 업데이트 된 것 확인 후 추가적인 DOM조작할 때
    // 혹은 데이터 변경 후 특정 DOM 요소의 최종 상태 기반으로 계산 및 조작 수행 시 사용
    inputRef.value.focus();
  });
};
const listUpdate = () => {
  emit("list-update", copyPropsItem.value);
  editMode.value = false;
};
</script>

<template>
  <li
    role="listitem"
    class="todo-list"
    :class="{ complete: props.item.complete }"
    v-if="!editMode">
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
        role="button"
        @click="editModeChange"></i>
      <i
        class="fa-solid fa-trash-can"
        aria-label="삭제"
        role="button"
        @click="listDelete"></i>
    </div>
  </li>
  <li v-else class="todo-list edit" role="listitem">
    <div class="todo-list__left">
      <input
        ref="inputRef"
        type="text"
        role="textbox"
        placeholder="할 일을 수정하세요."
        :value="copyPropsItem.text"
        @input="copyPropsItem.text = $event.target.value"
        @keydown.enter="listUpdate" />
    </div>
    <div class="todo-list__right">
      <i
        class="fa-regular fa-circle-check"
        aria-label="수정 저장"
        @click="listUpdate"></i>
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

  &.edit {
    background-color: rgba(0, 128, 128, 0.161);
    & input {
      width: 100%;
      border: none;
      background-color: transparent;
    }
  }

  .todo-list__left {
    display: flex;
    width: 100%;
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
