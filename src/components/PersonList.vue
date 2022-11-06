<script setup lang="ts">
import { Person } from '../components/Persons.vue'

type Props = {
  persons: Person[]
}

defineProps<Props>()
const emit = defineEmits(['delete'])

const onClickDelete = (id: number, name: string) => {
  if (confirm('Delete ' + name + '?')) {
  emit('delete', id)
  }
}
</script>

<template>
 <li v-for="person in persons" :key="person.id" class="person-list">
  <span>{{ person.name }}</span>
  <span>age:{{ person.age }}</span>
  <button @click="onClickDelete(person.id, person.name)" class="delete-btn">
    <span>delete</span>
  </button>
 </li>
</template>

<style scoped>
.person-list {
  list-style: none;
  margin: 12px;
  border-radius: 4px;
  font-size: 20px;
  align-items: center;
  display: flex;
  justify-content: space-between;
  background-color: rgb(85, 179, 179);
  padding: 8px 20px;
  width: 300px;
  font-weight: bold;
}

.delete-btn {
  padding: 8px 10px;
  font-size: 16px;
}
</style>