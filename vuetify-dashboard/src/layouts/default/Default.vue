<script setup>
import {ref} from 'Vue';
const drawer = ref(false);
</script>

<template>
<v-layout class="rounded rounded-md">
  <!-- location="bottom/top" -->
  <!-- density="compact/comfortable/prominent(biggest)" -->
  <!-- :color="`#111111`" -->
  <!-- :elevation="20" shadow-height -->
  <v-app-bar>
    <template #prepend>
      <v-app-bar-nav-icon
        variant="text"
        @click.stop="drawer = !drawer"
      ></v-app-bar-nav-icon>
      <v-toolbar-title>
        <router-link to="/"
          class="text-decoration-none text-blue"
        > 
          MDUI DASHBOARD 
        </router-link>
      </v-toolbar-title>
    </template>
    <template #append>
      <v-menu>
        <template v-slot:activator="{ props }">
          <v-avatar 
            size="50"
            color="blue"
            v-bind="props"
            >
            <span>AS</span>
          </v-avatar>
        </template>
        <v-list>
          <v-list-item
            v-for="(item, index) in [
              'Profile',
              'Settings',
              'Logout'
            ]"
            :key="index"
            :value="index"
          >
            <v-list-item-title>{{ item }}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </template>
  </v-app-bar>

  <v-navigation-drawer
    rail
    expand-on-hover
    v-model="drawer"
  >
    <v-list>
      <v-list density="compact" nav>
          <v-list-item prepend-icon="mdi-note-outline" 
            title="Posts"
            :to="`/posts`"
          ></v-list-item>
          <v-list-item prepend-icon="mdi-comment-outline" 
            title="Comments"
            :to="`/comments`"
            ></v-list-item>
        </v-list>
    </v-list>
  </v-navigation-drawer>

  <v-main class="d-flex align-center justify-center" 
    style="min-height: 300px;">
  <router-view></router-view>
  </v-main>
</v-layout>
</template>