<script setup lang="ts">
import { ref, Ref } from "vue"
import PersonList from './PersonList.vue';
import PersonPostFormVue from './PersonPostForm.vue';

export type Person = {
  id: number,
  name: string,
  age: number,
}

const persons: Ref<Person[]> = ref([{ id: 0, name: 'John', age: 24 }, { id: 1, name: 'Mike', age: 18 }])

const registerPerson = (person: Person) => {
  persons.value.push(person)
}

const deletePerson = (id: number) => {
  persons.value = persons.value.filter(p => p.id !== id)
}

</script>

<template>
  <div class="container">
    <div><img src="../../src/assets/icon.jpeg"></div>
    <h1>List of Personal Information</h1>
    <PersonPostFormVue @register="registerPerson" />
    <div class="list-container">
      <ul>
        <PersonList :persons="persons"  @delete="deletePerson"/>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

ul {
  padding: 0;
}

h1 {
  font-size: 36px;
}

img {
  width: 100%;
}

</style>