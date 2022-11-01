<template>

</template>
<script>

import firebase from "firebase";

export default {

  beforeMount(){

    console.log("woohooo it loaded");

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
      showAlert: false,
      formData: {
        name: "",
        email: "",
        message: "",
      },
      items: []
    };
  },
  methods: {

    async sendMessage(e) {
      const self = this;
      var data = new FormData();

      data.append("Name", self.formData.name);
      data.append("Email", self.formData.email);
      data.append("Message", self.formData.message);

      fetch("https://formspree.io/f/mvodbwva", {
        method: "POST",
        body: data,
        headers: {
          Accept: "application/json",
        },
      }).then((response) => {
        if (response.ok) {
          this.showAlert = true;
          form.reset();
        } else {
          alert("Sending message failed, please try again");
        }
      });
      // .catch(error => {
      //   alert("Sending message failed, please try again");
      // });
    },
  },
  head: {
    title: "My Priorities",
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
        content: "priorities",
      },
      {
        hid: "og:title",
        name: "og:title",
        content: "priorities",
      },
      {
        property: "og:description",
        content: "priorities",
      },
      {
        hid: "og:image",
        name: "og:image",
        content: require("@/assets/contact.jpg"),
      },
    ],
  },
};
</script>
<style scoped>
.container {
  margin-top: 120px;
}
form {
  margin-top: 40px;
  text-align: left;
}
</style>
