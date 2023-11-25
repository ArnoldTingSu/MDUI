<script setup lang="ts">
import {ref} from "vue";
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
        author: "Red"
    },
    {
        title: "Post 9", 
        author: "Yed"
    },
    {
        title: "Post 10", 
        author: "Jed"
    },
    {
        title: "Post 11", 
        author: "Edd"
    },
]);

const selected = ref([]);
const search = ref("")

</script>

<template>
    <div>
        <h1>POSTS!</h1>
        <v-text-field
        v-model="search"
        label="Search"
        prepend-inner-icon="mdi-magnify"
        single-line
        variant="outlined"
        hide-details
      ></v-text-field>
        <v-data-table 
            :items="posts"
            :headers="[
                {
                    title: 'Post Title',
                    align:'start',
                    sortable: false,
                    key: 'title'
                },
                {
                    title: 'Author',
                    align: 'end',
                    key: 'author'
                }
            ]"
            show-select
            item-value="title"
            v-model="selected"
            :search="search"
        ></v-data-table>
    </div>
</template>