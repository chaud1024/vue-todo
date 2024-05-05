<script setup>
import { ref } from "vue";

import Input from "@/components/Input.vue";

const listItem = ref([]);
const addListItem = (text) => {
  console.log("list item 추가");
  const newItem = {
    id: Math.random(),
    text: text,
    complete: false,
  };
  listItem.value.push(newItem);
};
</script>
<template>
  <Input @add-list="addListItem" />
  <div v-if="listItem.length == 0">
    <p>할 일이 없습니다! 새로운 할 일을 생성하세요.</p>
  </div>
  <ul v-if="listItem.length > 0">
    <li v-for="item in listItem" :key="item.id">
      {{ item.text }}
    </li>
  </ul>
</template>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>
