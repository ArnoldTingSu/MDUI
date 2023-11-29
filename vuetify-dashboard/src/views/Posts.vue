<script setup lang="ts">
import {ref} from "vue";
import PostForm from "@/components/PostForm.vue";
import { refAutoReset } from '@vueuse/core'
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
const postForm = ref();

const postSaved = refAutoReset(false, 4000);

function handleClickOutside() {
    selected.value = [];
}

type densities = "default" | "compact" | "comfortable"
const tableDensity = ref<densities>("default");

function handleResize() {
    let density: densities = "default";
    if (window.innerHeight < 800) density = "comfortable";
    if (window.innerHeight < 600) density = "compact";
    tableDensity.value = density;
}
</script>

<template>
<div>
    <!-- alert styles v-alert vs snackbar -->

    <v-alert
        variant="tonal"
        type="success"
        closable
        title="Post Updated"
        v-model="postSaved"
    />

    <!-- // <v-snackbar v-model="postSaved" :timeout="4000">
    //     <div class="d-flex align-center">
    //         <v-icon icon="mdi-check" class="text-green pr-3"></v-icon>
    //         Post Saved!
    //     </div>
    // </v-snackbar> -->

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
        v-click-outside="handleClickOutside"
        v-resize="handleResize"
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
        :density="tableDensity"
    >
    <template v-slot:item.title="{ item }" >
    <v-dialog fullscreen>
        <template v-slot:activator="{ props }">
        <button
            v-ripple class="pa-3"
            v-bind="props"
        >
            {{item.title}}
        </button>
        </template>
    <template v-slot:default="{ isActive }">
        <v-card>
            <v-card-title class="text-h5 grey lighten-2">
                Edit Post
            </v-card-title>
            <v-card-text>
                <PostForm 
                ref="postForm" 
                :post="item"
                @submit="
                    isActive.value= false
                    postSaved = true;
                "
                />
            </v-card-text>
        <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn
                text="Cancel"
                @click="isActive.value = false"
                >
            </v-btn>
            <v-btn
                color="blue"
                text="Save Post"
                variant="flat"
                @click="postForm.submit()">

            </v-btn>
        </v-card-actions>
        </v-card>     
    </template>
    </v-dialog>
    </template>
    </v-data-table>
</div>
</template>