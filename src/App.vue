<template>
  <v-app id="inspire">
    <v-navigation-drawer :mobile-breakpoint="768" v-model="drawer" app>
      <v-card class="mx-auto" max-width="434">
        <v-img
          gradient="to top right, rgba(19,84,122,.5), rgba(108,36,199,.8)"
          :height="$route.path === '/' ? '260' : '200'"
          src="todo2.png"
        >
          <v-container class="pt-84">
            <v-avatar class="profile" size="100">
              <v-img src="eren.png" alt="Erencan Cabuk"></v-img>
            </v-avatar>

            <div class="white--text text-subtitle-1">Erencan Cabuk</div>
            <v-btn
              v-for="footer in footers"
              :key="footer.icon"
              class="white--text"
              icon
              :href="footer.link"
            >
              <v-icon size="32px">
                {{ footer.icon }}
              </v-icon>
            </v-btn>
          </v-container>
        </v-img>
      </v-card>
      <v-list class="pt-6" dense nav>
        <v-list-item v-for="item in items" :key="item.title" :to="item.to" link>
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      app
      color="purple"
      dark
      src="todo4.png"
      prominent
      :height="$route.path === '/' ? '260' : '200'"
    >
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"
        ></v-img>
      </template>

      <v-container class="header-container pa-0 pt-2">
        <v-row>
          <!-- Drawer -->
          <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
          <v-spacer></v-spacer>
          <!-- Search -->
          <search />
        </v-row>
        <v-row>
          <v-app-bar-title class="barTitle text-h4 ml-4">
            Your
          </v-app-bar-title>
        </v-row>
        <v-row>
          <v-app-bar-title class="barTitle text-h4 ml-4">
            Things
          </v-app-bar-title>
        </v-row>
        <v-row>
          <!-- Live Date Time -->
          <live-date-time />
        </v-row>
        <v-row v-if="$route.path === '/'">
          <!-- FieldAddTaskComponent -->
          <field-add-task />
        </v-row>
      </v-container>
    </v-app-bar>

    <v-main>
      <!--  -->
      <router-view></router-view>
      <snackbar />
    </v-main>
  </v-app>
</template>

<script>
import Snackbar from "./components/Shared/Snackbar.vue";
import FieldAddTask from "./components/Todo/FieldAddTask.vue";
import LiveDateTime from "./components/Tools/LiveDateTime.vue";
import Search from "./components/Tools/Search.vue";

export default {
  components: { Snackbar, Search, LiveDateTime, FieldAddTask },
  data: () => ({
    footers: [
      {
        icon: "mdi-linkedin",
        link: "https://www.linkedin.com/in/erncncbk/",
      },
      {
        icon: "mdi-github",
        link: "https://github.com/erncncbk",
      },
    ],
    drawer: true,
    items: [
      { title: "Todo", icon: "mdi-format-list-checks", to: "/" },
      { title: "About", icon: "mdi-help-box", to: "/about" },
    ],
    right: null,
  }),
  mounted() {
    // console.log(this.$route.name);
    this.$store.dispatch("getTasks");
  },
};
</script>

<style lang="sass">
.header-container
  max-width: none !important
.v-app-bar-title__content
  width: 100% !important
  max-width: none !important
</style>