<template>
<v-layout class="rounded rounded-md">
  <!-- location="bottom/top" -->
  <!-- density="compact/comfortable/prominent(biggest)" -->
  <!-- :color="`#111111`" -->
  <!-- :elevation="20" shadow-height -->
  <v-app-bar title="Application bar">
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
  >
    <v-list>
      <v-list density="compact" nav>
          <v-list-item prepend-icon="mdi-folder" title="Posts" value="myfiles"></v-list-item>
          <v-list-item prepend-icon="mdi-folder" title="Comments" value="myfiles"></v-list-item>
          <v-list-item prepend-icon="mdi-account-multiple" title="Shared with me" value="shared"></v-list-item>
          <v-list-item prepend-icon="mdi-star" title="Starred" value="starred"></v-list-item>
        </v-list>
    </v-list>
  </v-navigation-drawer>

  <v-main class="d-flex align-center justify-center" 
    style="min-height: 300px;">
  <router-view></router-view>
  </v-main>
</v-layout>
</template>