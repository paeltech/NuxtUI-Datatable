<script setup>
const people = [
  {
    id: 1,
    name: 'Lindsay Walton',
    title: 'Front-end Developer',
    email: 'lindsay.walton@example.com',
    role: 'Member',
  },
  {
    id: 2,
    name: 'Courtney Henry',
    title: 'Designer',
    email: 'courtney.henry@example.com',
    role: 'Admin',
  },
  {
    id: 3,
    name: 'Tom Cook',
    title: 'Director of Product',
    email: 'tom.cook@example.com',
    role: 'Member',
  },
  {
    id: 4,
    name: 'Whitney Francis',
    title: 'Copywriter',
    email: 'whitney.francis@example.com',
    role: 'Admin',
    sortable: true,
  },
  {
    id: 5,
    name: 'Leonard Krasner',
    title: 'Senior Designer',
    email: 'leonard.krasner@example.com',
    role: 'Owner',
  },
  {
    id: 6,
    name: 'Floyd Miles',
    title: 'Principal Designer',
    email: 'floyd.miles@example.com',
    role: 'Member',
  },
];

const columns = [
  {
    key: 'id',
    label: 'ID',
  },
  {
    key: 'name',
    label: 'User name',
    sortable: true,
  },
  {
    key: 'title',
    label: 'Job position',
    sortable: true,
  },
  {
    key: 'email',
    label: 'Email',
  },
  {
    key: 'role',
  },
];

const q = ref('');
const page = ref(1);
const pageCount = 3;
const filteredRows = computed(() => {
  if (!q.value) {
    return people.slice((page.value - 1) * pageCount, page.value * pageCount);
  }
  return people.filter((person) => {
    return Object.values(person).some((value) => {
      return String(value).toLowerCase().includes(q.value.toLowerCase());
    });
  });
});
</script>
<template>
<UContainer class="mt-16">
  <UInput v-model="q" placeholder="Filter people..." />
  <UTable :columns="columns" :rows="filteredRows" :sort="{ column: 'title' }" />
  <UPagination v-model="page" :page-count="pageCount" :total="people.length" class="mt-8" />
</UContainer>
</template>
