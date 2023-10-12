<template>
  <v-card>
    <v-layout style="background-color: #bbdefb">
      <v-app-bar color="#2D3047" prominent>
        <v-toolbar-title>TodoList & Chart</v-toolbar-title>

        <v-spacer></v-spacer>

        <v-btn
          v-if="!isLogin"
          variant="text"
          icon="mdi-login"
          @click="isLogin = true"
        ></v-btn>

        <v-menu v-else>
          <template v-slot:activator="{ props }">
            <v-btn variant="tonal">
              <div class="mr-5" v-bind="props">
                <v-avatar size="30" class="mr-3">
                  <v-img
                    src="https://images.hdqwalls.com/download/disney-loki-r6-50x50.jpg"
                  /> </v-avatar
                ><span style="font-size: 12px">John Doe</span>
              </div>
            </v-btn>
          </template>
          <v-list>
            <v-list-item
              v-for="(item, index) in items"
              :key="index"
              :value="index"
            >
              <v-list-item-title @click="isLogin = false">{{
                item.title
              }}</v-list-item-title>
            </v-list-item>
          </v-list>
        </v-menu>
      </v-app-bar>

      <v-navigation-drawer
        color="#2D3047"
        v-model="drawer"
        :rail="isSmallScreen ? true : rail"
        permanent
        @click="rail = false"
      >
        <v-list-item
          v-if="!isSmallScreen"
          prepend-icon="mdi-menu"
          :title="isLogin ? 'John Doe' : 'Unknow'"
          class="ml-2"
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
          ><RouterLink to="/" style="text-decoration: none; color: #93b7be">
            <v-list-item
              :class="{ 'active-item': $route.path === '/' }"
              prepend-icon="mdi-list-status"
              title="TodoList"
              value="todoList"
            ></v-list-item>
          </RouterLink>
          <RouterLink to="/chart" style="text-decoration: none; color: #93b7be">
            <v-list-item
              :class="{ 'active-item': $route.path === '/chart' }"
              prepend-icon="mdi-chart-areaspline"
              title="Chart"
              value="chart"
            ></v-list-item>
          </RouterLink>
        </v-list>
      </v-navigation-drawer>
      <v-main class="mx-lg-auto" style="overflow-y: auto"
        ><v-col cols="12"><RouterView /></v-col
      ></v-main>
    </v-layout>
  </v-card>
</template>

<script lang="ts">
export default {
  data() {
    return {
      drawer: true,
      rail: true,
      isLogin: false,
      items: [{ title: "Logout" }],
      isSmallScreen: false,
    };
  },
  created() {
    window.addEventListener("resize", this.checkScreenSize);
    this.checkScreenSize(); // Initial check
  },
  methods: {
    checkScreenSize() {
      this.isSmallScreen = window.innerWidth <= 1080;
    },
  },
};
</script>

<style scoped>
.active-item {
  background-color: #3e455a;
}
</style>
