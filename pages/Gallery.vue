<template>
    <!-- <b-row class="justify-content-center"> -->
      <!-- <b-col cols="md-6"> -->
        <div class="db-images-div">
          <img v-for="item in items" :src="item" class="db-images"/>        
        </div>
      <!-- </b-col> -->
    <!-- </b-row> -->
</template>
<script>

import firebase from "firebase";

export default {

  beforeMount(){
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

    // firebase.firestore().collection("gallery").doc(imageUpload.name).set({"url": this.img1});

    let imageUrls = [];

    firebase.firestore().collection("gallery").get().then((querySnapshot) => {
      querySnapshot.forEach((doc) =>{
        imageUrls.push(
          "<img src='" + doc.data().url + "' >"
        );
      });
    })

    console.log(imageUrls);
    // document.getElementById("images") = imageUrls;
    // imagesDiv = imageUrls;
    this.getImageUrls();
    
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

    getImageUrls(){

    //   const firebaseConfig = {
    //   apiKey: "AIzaSyBBuwx72mUae9AumjHf7Rjsz7iaU70ZK0o",
    //   authDomain: "vawwebsite-72bd9.firebaseapp.com",
    //   projectId: "vawwebsite-72bd9",
    //   storageBucket: "vawwebsite-72bd9.appspot.com",
    //   messagingSenderId: "798885086728",
    //   appId: "1:798885086728:web:26f36f94c31cd1628433bd"
    // };

    //   if (!firebase.apps.length) {
    //     firebase.initializeApp(firebaseConfig);
    //   }else {
    //     firebase.app(); // if already initialized, use that one
    //   }


      let imageUrls = [];

      firebase.firestore().collection("gallery").get().then((querySnapshot) => {
        querySnapshot.forEach((doc) =>{
          imageUrls.push(
            doc.data().url
          );
        });
      })

      this.items = imageUrls;
      console.log(this.items);

    },

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
    title: "Gallery",
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
        content: "Gallery",
      },
      {
        hid: "og:title",
        name: "og:title",
        content: "Gallery",
      },
      {
        property: "og:description",
        content: "Gallery",
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
.line-after {
  overflow: hidden;
}
.line-after::after {
  content: "";
  display: inline-block;
  height: 0.5em;
  vertical-align: bottom;
  width: 100%;
  margin-right: -100%;
  margin-left: 10px;
  border-top: 2px solid #8f00ff;
}
</style>
