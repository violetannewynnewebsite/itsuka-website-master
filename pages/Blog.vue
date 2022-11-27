<template>
  <div class="container animate__animated animate__fadeIn">

    <h1 align="left" class="line-after">Blogs</h1>
      
    <div v-for="blog in blogs" style="font-size:22px;">
          <button @click="displayBlog(blog.title)" class="accordion">{{blog.title}}</button>
          <div :id="blog.title" class="panel">
            <h5>{{blog.date}}</h5>
            <p>{{blog.text}}</p>
          </div>
        </div>
  </div>
</template>
<script>

import firebase from "firebase";

export default {

  mounted(){
  },

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

    this.getBlogs();

  },

  data() {
    return {
      showAlert: false,
      blogs: []
    };
  },
  methods: {
    getBlogs() {
        firebase.firestore().collection("blogs").get().then((querySnapshot) => {
        querySnapshot.forEach((doc) =>{
          this.blogs.push({
            title: doc.data().title,
            date: doc.data().date,
            text: doc.data().text
          }
          );
        });
      })
    },
    displayBlog(id){
      if(document.getElementById(id).style.display == "block"){
        document.getElementById(id).style.display = "none";
      }
      else{
        document.getElementById(id).style.display = "block";
      }
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
    title: "Blog",
    link: [
             {
                 rel: "icon",
                 href: require("../assets/signatureInitials.png")
             },
          ],
    meta: [
      {
        hid: "Blog",
        name: "Blog",
        content: "Blog",
      },
      {
        hid: "og:title",
        name: "og:title",
        content: "Blog",
      },
      {
        property: "Blog",
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
.accordion {
  background-color: #eee;
  color: #444;
  cursor: pointer;
  padding: 18px;
  width: 100%;
  text-align: left;
  border: none;
  outline: none;
  transition: 0.4s;
}
.active, .accordion:hover {
  background-color: #8f00ff;
}
.panel {
  padding: 0 18px;
  background-color: transparent;
  display: none;
  overflow: hidden;
}
</style>
