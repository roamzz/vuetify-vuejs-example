<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <v-toolbar-title>Vuetify Dashboard</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn
        v-for="link in links"
        :key="`${link.label}-header-link`"
        text
        rounded
        :to="link.url"
      >
        {{ link.label }}
      </v-btn>
      <v-btn @click="toggleTheme" text rounded>
        Toggle Theme
      </v-btn>
    </v-app-bar>

    <v-content>
     <!--<transition name="fade" mode="out-in">-->
    <transition name="slide-fade" mode="out-in">
      <router-view></router-view>
    </transition>
    </v-content>
    <v-footer color="primary lighten-1" padless>
      <v-layout justify-center wrap>
        <v-btn
          v-for="link in links"
          :key="`${link.label}-footer-link`"
          color="white"
          text
          rounded
          class="my-2"
          :to="link.url"
        >
          {{ link.label }}
        </v-btn>
        <v-flex primary lighten-2 py-4 text-center white--text xs12>
          {{ new Date().getFullYear() }} — <strong>Vuetify</strong>
        </v-flex>
      </v-layout>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: "App",

  components: {},
  data() {
    return {
      links: [
        {
          label: "Home",
          url: "/"
        },
        {
          label: "Login",
          url: "/login"
        },
        {
          label: "Dashboard",
          url: "/dashboard"
        },
        {
          label: "Sign Up",
          url: "/signup"
        },
        {
          label: "Weather",
          url: "/weather"
        }
      ]
    };
  },
  methods: {
    toggleTheme() {
      this.$vuetify.theme.themes.dark.anchor = "#41B883";
      this.$vuetify.theme.dark = !this.$vuetify.theme.dark;
    }
  }
};
</script>


<style lang="scss" scoped>
.slide-fade-enter {
      transform: translateX(10px);
      opacity: 0;
    }

    .slide-fade-enter-active,
    .slide-fade-leave-active {
      transition: all 0.2s ease;
    }

    .slide-fade-leave-to {
      transform: translateX(-10px);
      opacity: 0;
    }

.slide-up-enter {
      transform: translateX(10px);
      opacity: 0;
    }

    .slide-up-enter-active {
      transition: all 0.2s ease;
    }

    .slide-up-move {
      transition: transform 0.5s ease-out;
    }

</style>
