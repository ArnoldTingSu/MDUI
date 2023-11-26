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
    >
    <template #item.title="{ item }">
    <v-dialog
        fullscreen
    >
        <template v-slot:activator="{ props }">
        <button
            v-bind="props"
        >
            {{item.title}}
        </button>
        </template>
    <template v-slot:default="{ isActive }">
        <v-card>
        <v-card-title class="text-h5 grey lighten-2">
            Privacy Policy
        </v-card-title>

        <v-card-text>
            Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
            <v-spacer></v-spacer>
            <button
                color="primary"
                text
                @click="isActive.value = false"
                >
                I accept
            </button>
        </v-card-actions>
        </v-card>     
    </template>
    </v-dialog>
    </template>
    </v-data-table>
</div>
</template>