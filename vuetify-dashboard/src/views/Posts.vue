<script setup lang="ts">
import {ref} from "vue";
import PostForm from "@/components/PostForm.vue";
import { refAutoReset } from '@vueuse/core'
//Item rarity
// 0 - poor     // 1 - common 
// 2 - uncommon // 3 - rare 
// 4 - epic     // 5 - legendary
const warItem = ref([
    {
        itemName: "Hearthstone",
        itemRarity: 1,
        lootType: "Soulbound",
        unique: true,
        slot: null,
        itemType: null,
        damage: [],
        weaponSpeed: null,
        damagePerSec: null,
        primaryStats: [],
        levelRequire: null,
        effect: ['Use: Returns you home. Speak with an Innkeeper in a different place to change your home location.'],
        flavorText: '',
    },
]);

const selected = ref([]);
const search = ref("")

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
			:items="warItem"
			:headers="[
					{
							title:'Item Name',
							align:'start',
							sortable: false,
							key: 'itemName'
					},
					{
							title:'Effect',
							align:'start',
							sortable: false,
							key: 'effect[0]'
					},
					]"
			show-select
			item-value="itemName"
			v-model="selected"
			:search="search"
			:density="tableDensity"
    >
    <template v-slot:title="{ items }" >
        <button
            v-ripple class="pa-3"
            v-bind="items"
        >
            {{items.itemName}}
        </button>
    </template>
    </v-data-table>
		<v-tooltip 
		icon-
		>
  <template v-slot:activator="{ warItem }">
    <v-btn 
		v-slot:default="items"
			>
			<v-icon
              icon="mdi-view-dashboard"
              size="large"
				/>
		</v-btn>
  </template>
</v-tooltip>
</div>
</template>