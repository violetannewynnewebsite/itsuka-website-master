<template>
  <b-row style="margin-left: 0; margin-right: 0">
    <b-col md="4">
      <b-img
        src="../assets/Violet-Anne_Wynne_2020.jpg"
        id="avatar-img"
        alt="Itsuka"
        class="profile-pic"
      />
    </b-col>

    <b-col md="8">
      <h2 class="intro animate__animated animate__fadeInUp animate__fast">
        Hi!,
        <br />I<span>'m Violet-Anne Wynne</span>.
      </h2>

      <div class="col-md-10 info">
        A TD from Clare who's passionate about working for the people!
        <br />
        <b-button
          class="action-btn animate__animated animate__wobble animate__delay-4s animate__fast"
          to="/about"
        >
          Explore >
        </b-button>

        <b-button
          class="action-btn"
          to="/contact"
          variant="primary"
          target="_blank"
        >
          Get In Touch
        </b-button>

        <!-- .SOCIAL LINKS SECTION -->
        <div
          class="social-icons animate__animated animate__fadeInUp animate__delay-1s"
        >
          <social-link :to="socialLinks.twitter">
            <TwitterIcon />
          </social-link>
          <social-link :to="socialLinks.email">
            <MailIcon />
          </social-link>
        </div>
      </div>
    </b-col>
  </b-row>
</template>

<script>
import GithubIcon from "vue-ionicons/dist/logo-github.vue";
import LinkedinIcon from "vue-ionicons/dist/logo-linkedin.vue";
import TwitterIcon from "vue-ionicons/dist/logo-twitter.vue";
import FacebookIcon from "vue-ionicons/dist/logo-facebook.vue";
import YoutubeIcon from "vue-ionicons/dist/logo-youtube.vue";
import MailIcon from "vue-ionicons/dist/md-mail.vue";

import firebase from "firebase";

export default {
  components: {
    GithubIcon,
    LinkedinIcon,
    TwitterIcon,
    FacebookIcon,
    YoutubeIcon,
    MailIcon
  },

  created(){

    const firebaseConfig = {
  apiKey: "AIzaSyAxJzN6RXxvNlt-QzEeRkWsxUx8sM08D4A",
  authDomain: "vawwebsite-65763.firebaseapp.com",
  projectId: "vawwebsite-65763",
  storageBucket: "vawwebsite-65763.appspot.com",
  messagingSenderId: "799341768510",
  appId: "1:799341768510:web:7589601ef9bbe77881866f"
};

    if (!firebase.apps.length) {
      firebase.initializeApp(firebaseConfig);
    }else {
      firebase.app(); // if already initialized, use that one
    }
  },

  data() {
    return {
      avatar: require("@/assets/avatar-1.webp"),
      // ADD YOUR SOCIAL LINKS HERE 👇
      socialLinks: {
        twitter: "https://twitter.com/WynneTd",
        email:"mailto:violet-anne.wynne@oireachtas.ie",

      },
    };
  },

  head: {
    title: "Violet-Anne Wynne",
    link: [
             {
                 rel: "icon",
                 href: require("../assets/signatureInitials.png")
             },
          ],
    meta: [
      {
        hid: "description",
        name: "description",
        content:
          "",
      },
      {
        hid: "og:title",
        name: "og:title",
        content: "Violet-Anne Wynne",
      },
      {
        property: "og:description",
        content:
          "",
      },
      {
        hid: "og:image",
        name: "og:image",
        content: "../assets/sf-logo.png",
      },
    ],
  },
  mounted() {
    this.$nextTick(() => {
      this.$nuxt.$loading.start();

      setTimeout(() => this.$nuxt.$loading.finish(), 500);
    });
  },
};
</script>
