<template>
  <b-navbar toggleable="lg" fixed="top" type="light" variant="light">
    <a class="logo" href="/">
      <img class="logo" src="../assets/signature.png">
    </a>
    <!-- <b-navbar-brand tag="h1" to="/" style="font-weight: bolder"
      >Violet-Anne Wynne</b-navbar-brand
    > -->
    <b-navbar-toggle
      target="nav-collapse"
      style="border-radius: 0"
    ></b-navbar-toggle>

    <b-collapse
      id="nav-collapse"
      is-nav
      class="animate__animated animate__fadeInDown"
    >
      <b-navbar-nav>
        <b-nav-item to="/">Home</b-nav-item>
        <b-nav-item to="/about">About</b-nav-item>
        <b-nav-item to="/gallery">Gallery</b-nav-item>
        <b-nav-item to="/articles">Latest News</b-nav-item>
        <b-nav-item to="/priorities">My Priorities</b-nav-item>
        <b-nav-item to="/blog">Blog</b-nav-item>
        <b-nav-item to="/contact">Contact Me</b-nav-item>
        <!-- <b-nav-item
          href="#"
          v-if="themeMode == 'dark'"
          @click="toggleDarkMode"
          class="moon-icon"
          title="Toggle Darkmode"
        >
          <SunnyIcon style="color: #eee; font-size: 20px" />
        </b-nav-item>
        <b-nav-item
          href="#"
          v-else
          @click="toggleDarkMode"
          class="moon-icon"
          title="Toggle Darkmode"
        >
          <MoonIcon style="color: #000; font-size: 20px" />
        </b-nav-item> -->
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
</template>

<script>
require("vue-ionicons/ionicons.css");
import SunnyIcon from "vue-ionicons/dist/md-sunny.vue";
import MoonIcon from "vue-ionicons/dist/md-moon.vue";
export default {
  name: "NavBar",
  components: {
    SunnyIcon,
    MoonIcon,
  },
  data() {
    return {
      themeMode: "",
    };
  },
  methods: {
    toggleDarkMode() {
      if (
        localStorage.themeMode !== undefined &&
        localStorage.themeMode != "dark"
      ) {
        localStorage.themeMode = "dark";
        document.body.classList.toggle("dark");
        document.querySelector("nav").classList.toggle("navbar-light");
        document.querySelector("nav").classList.toggle("bg-light");
        document.querySelector("nav").classList.toggle("navbar-dark");
        document.querySelector("nav").classList.toggle("bg-dark");
        this.themeMode = "dark";
      } else {
        localStorage.themeMode = "light";
        document.body.classList.toggle("dark");
        this.themeMode = "light";
        document.querySelector("nav").classList.toggle("navbar-dark");
        document.querySelector("nav").classList.toggle("bg-dark");
        document.querySelector("nav").classList.toggle("navbar-light");
        document.querySelector("nav").classList.toggle("bg-light");
      }
    },
  },
  mounted() {
    this.themeMode = localStorage.themeMode;
  },
};
</script>
<style scoped>
.navbar-nav {
  margin-left: 100px;
}
@media screen and (max-width: 420px) {
  .navbar-nav {
    margin-left: 0px;
  }
}
.nav-item {
  font-size: 20px;
  margin: 15px;
  border-radius: 2px;
}
.nav-link a {
  color: #000;
  text-decoration: none;
}
.nav-link:hover a{
  color:#8f00ff;
} 
.nav-item:hover {
  background: #ffffff;
}
.moon-icon {
  color: #000;
}
.moon-icon:hover {
  background: transparent !important;
}
.bg-light {
  background-color: #ffffff !important;
}
</style>
