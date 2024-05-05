<script setup>
import { ref } from "vue";

import Input from "@/components/Input.vue";
import ListItem from "@/components/ListItem.vue";

const listItem = ref([]);
const addListItem = (text) => {
  console.log("list item 추가");
  const newItem = {
    id: Math.floor(Math.random() * 100),
    text: text,
    complete: false,
  };
  listItem.value.push(newItem);
};

const listItemComplete = (item) => {
  // console.log(listItem.value);
  listItem.value = listItem.value.map((v) =>
    v.id === item.id ? { ...v, complete: !v.complete } : v,
  );
  // console.log(listItem.value);
};

const listItemDelete = (item) => {
  listItem.value = listItem.value.filter((v) => v.id !== item.id);
};

const listClear = () => {
  listItem.value = [];
};
</script>
<template>
  <Input @add-list="addListItem" />
  <div v-if="listItem.length == 0">
    <p>할 일이 없습니다! 새로운 할 일을 생성하세요.</p>
  </div>
  <ul v-if="listItem.length > 0">
    <ListItem
      v-for="item in listItem"
      :key="item.id"
      :item="item"
      @list-complete="listItemComplete"
      @list-delete="listItemDelete" />
  </ul>
  <button @click="listClear">목록 삭제</button>
</template>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>
