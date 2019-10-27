<template>
  <nav>
    <v-navigation-drawer v-model="drawer" app clipped>
      <v-card class="mx-auto" width="300">
        <v-list>
          <v-list-item link router to="/">
            <v-list-item-icon>
              <v-icon>mdi-home</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Home</v-list-item-title>
          </v-list-item>
          <v-list-group
            v-for="app in apps"
            :key="app.appName"
            router
            :to="app.route"
            value="true"
          >
            <template v-slot:activator>
              <v-list-item-title>{{ app.appName }}</v-list-item-title>
            </template>

            <v-list-item
              v-for="(app, i) in app.subApps"
              :key="i"
              link
              router
              :to="app.route"
            >
              <v-list-item-title v-text="app.appName"></v-list-item-title>
            </v-list-item>
          </v-list-group>
        </v-list>
      </v-card>
    </v-navigation-drawer>
    <v-app-bar app clipped-left dense>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer">
        <v-icon color="grey darken-1">mdi-menu</v-icon>
      </v-app-bar-nav-icon>
      <v-toolbar-title class="mr-12 align-center">
        <span class="title">PhotoStudio Cloud</span>
      </v-toolbar-title>
      <div class="flex-grow-1"></div>
      <v-menu left bottom>
        <template v-slot:activator="{ on }">
          <v-btn icon v-on="on">
            <v-icon>mdi-account-circle</v-icon>
          </v-btn>
        </template>

        <v-list>
          <v-list-item
            v-for="(menu, i) in accountMenu"
            :key="i"
            link
            router
            :to="menu.route"
          >
            <v-list-item-title>{{ menu.appName }}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>
  </nav>
</template>

<script>
export default {
  component: {
    name: "Nav"
  },

  data() {
    return {
      drawer: false,
      apps: [
        {
          route: "/app1",
          icon: "",
          appName: "app1",
          subApps: [
            { route: "/app1/link1/", icon: "", appName: "app1" },
            { route: "/app1/link2/", icon: "", appName: "app2" }
          ]
        },
        {
          route: "/app2",
          icon: "",
          appName: "app2",
          subApps: [
            {
              route: "/app2/link1/",
              icon: "",
              appName: "app2"
            },
            {
              route: "/app2/link2/",
              icon: "",
              appName: "Prova2"
            }
          ]
        }
      ],
      accountMenu: [
        {
          route: "/account/login/",
          icon: "mdi-account-box",
          appName: "Login"
        },
        {
          route: "/account/profile",
          icon: "mdi-account-box",
          appName: "profile"
        }
      ]
    };
  }
};
</script>

<style></style>
