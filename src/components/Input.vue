<script setup>
import { ref } from "vue";

const inputText = ref("");

const emit = defineEmits(["add-list"]);

const addTodo = (e) => {
  // 할 일 추가
  if (!e.isComposing && inputText.value.trim() !== "") {
    emit("add-list", inputText.value);
  }
  inputText.value = "";
};
</script>
<template>
  <div class="add-todo">
    <input
      type="text"
      id="addTodo"
      placeholder="할 일을 입력하세요"
      :value="inputText"
      @input="inputText = $event.target.value"
      @keydown.enter="addTodo" />
    <button @click="addTodo"><i class="fa-solid fa-plus"></i> 더하기</button>
  </div>
</template>

<style scoped>
.add-todo {
  width: 100%;
  position: relative;
  padding: 10px 0;

  & input {
    width: 100%;
    height: 100%;
    padding: 8px 10px;
    border: 1px solid transparent;
    border-bottom: 2px solid teal;
    background-color: transparent;
  }

  & button {
    position: absolute;
    top: 50%;
    right: 0;
    transform: translateY(-50%);
    border: none;
    background-color: transparent;
    cursor: pointer;
    padding: 6px 5px;

    &:hover {
      background-color: teal;
      color: white;
    }
  }
}
</style>
