<script setup lang="ts">
import {ref} from "Vue";
const posts = ref([
    {
        title: "Post 1", 
        author: "Fred"
    },
    {
        title: "Post 2", 
        author: "Bread"
    },
    {
        title: "Post 3", 
        author: "Sead"
    },
    {
        title: "Post 4", 
        author: "Kead"
    },
    {
        title: "Post 5", 
        author: "Head"
    },
    {
        title: "Post 6", 
        author: "Ked"
    },
    {
        title: "Post 7", 
        author: "Med"
    },
    {
        title: "Post 8", 
        author: "Zed"
    },
]);
</script>
<template>
    <div>
        <h1>POSTS!</h1>
        <v-table
        :height="300"
        :fixed-header="true"
        density="comfortable"
        :hover="true"
        >
    <thead>
      <tr>
        <th class="text-left">
          Name
        </th>
        <th class="text-left">
          Author
        </th>
      </tr>
    </thead>
    <tbody>
      <tr
        v-for="item in posts"
        :key="item.title"
      >
        <td>{{ item.title }}</td>
        <td>{{ item.author }}</td>
      </tr>
    </tbody>
  </v-table>
    </div>
</template>