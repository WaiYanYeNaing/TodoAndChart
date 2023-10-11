<template>
  <v-card>
    <v-layout>
      <v-navigation-drawer
        v-model="drawer"
        :rail="rail"
        permanent
        @click="rail = false"
      >
        <v-list-item
          prepend-avatar="https://randomuser.me/api/portraits/men/85.jpg"
          title="John Leider"
          nav
        >
          <template v-slot:append>
            <v-btn
              variant="text"
              icon="mdi-chevron-left"
              @click.stop="rail = !rail"
            ></v-btn>
          </template>
        </v-list-item>

        <v-divider></v-divider>

        <v-list density="compact" nav
          ><RouterLink to="/" style="text-decoration: none; color: black;">
            <v-list-item
              prepend-icon="mdi-home-city"
              title="TodoList"
              value="todoList"
            ></v-list-item>
          </RouterLink>
          <RouterLink to="/about" style="text-decoration: none; color: black;">
            <v-list-item
              prepend-icon="mdi-account"
              title="Chart"
              value="chart"
            ></v-list-item>
          </RouterLink>
        </v-list>
      </v-navigation-drawer>
      <v-main style="height: 100vh"><RouterView /></v-main>
    </v-layout>
  </v-card>
</template>

<!-- <template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template> -->

<script lang="ts">
import { RouterLink, RouterView } from "vue-router";
import HelloWorld from "./components/HelloWorld.vue";
export default {
  data() {
    return {
      drawer: true,
      rail: true,
    };
  },
};
</script>

<style scoped></style>
