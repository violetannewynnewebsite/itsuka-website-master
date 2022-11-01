<template>
  <b-container class="page animate__animated animate__fadeIn">
    <div id="loginForm">
      <input type="text" name="email" id="email" placeholder="Email"/>
      <input type="password" name="password" id="password" placeholder="Password"/>
      <button @click="login">Login</button>
    </div>

    <div id="pageContent" class="admin-content">
        <div>
          <h2>Gallery</h2>
          <input class="contentBtn" type="file" name="file" id="imageField" />
          <b-button class="contentUpload" @click="uploadImage">Upload</b-button>
          <h5>Delete Images</h5>
          <div v-for="image in galleryImages" class="accordion" :id="image.id">
            <p class="itemName">{{image.id}}</p>
            <b-button @click="deleteImage(image.id)" class="deleteBtn">Delete</b-button>
          </div>
        </div>
        <div>
          <h2>Upload Article</h2>
          <div class="contentForm">
            <input class="content" type="text" name="articleTitle" id="articleTitle" placeholder="Article Title"/>
            <input class="content" type="text" name="articleUrl" id="articleUrl" placeholder="Article URL"/>
            <input class="content" type="text" name="articleDesc" id="articleDesc" placeholder="Article Description"/>
            <input class="contentBtn" type="file" name="articleImage" id="articleImage" placeholder="Article Image"/>
            <b-button class="contentUpload" @click="uploadArticle">Upload</b-button>
            <h5>Delete Articles</h5>
            <div v-for="article in articles" class="accordion" :id="article.id">
              <p class="itemName">{{article.id}}</p>
              <b-button @click="deleteArticle(article.id, article.imageName)" class="deleteBtn">Delete</b-button>
            </div>
          </div>
        </div>
        <div>
          <h2>Upload Blog</h2>
          <div class="contentForm">
            <input class="content" type="text" name="blogTitle" id="blogTitle" placeholder="Blog Title"/>
            <input class="content" type="text" name="blogDate" id="blogDate" placeholder="Blog Date"/>
            <textarea class="content" name="blogText" id="blogText" placeholder="Blog Text" cols="50" rows="10"></textarea>
            <b-button class="contentUpload" @click="uploadBlog">Upload</b-button>
            <h5>Delete Blogs</h5>
            <div v-for="blog in blogs" class="accordion" :id="blog.id">
              <p class="itemName">{{blog.id}}</p>
              <b-button @click="deleteBlog(blog.id)" class="deleteBtn">Delete</b-button>
            </div>
          </div>
        </div>
    </div>
  </b-container>
</template>

<script>

import firebase from "firebase";

export default {
  data() {
    return {
      galleryImages: [],
      articles: [],
      blogs: []
    };
  },  
  
  created(){

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

  },

  methods: {

  getGalleryImages() {
        firebase.firestore().collection("gallery").get().then((querySnapshot) => {
        querySnapshot.forEach((doc) =>{
          this.galleryImages.push({
            id: doc.id
          }
          );
        });
      })
    },

  getBlogs() {
    firebase.firestore().collection("blogs").get().then((querySnapshot) => {
      querySnapshot.forEach((doc) =>{
        this.blogs.push({
          id: doc.id
        }
        );
      });
    })
  },

  getArticles() {
      firebase.firestore().collection("news").get().then((querySnapshot) => {
      querySnapshot.forEach((doc) =>{
        this.articles.push({
          id: doc.id,
          imageName: doc.data().imageName
        }
        );
      });
    })
  },

    async deleteImage(fileName){
      console.log(fileName)
      firebase.firestore().collection("gallery").doc(fileName).delete();
      firebase.storage().ref(`gallery/${fileName}`).delete();
      console.log("deleted");
      document.getElementById(fileName).style.display = "none";

    },

    async deleteArticle(articleTitle, imageName){
      console.log(articleTitle)
      firebase.firestore().collection("news").doc(articleTitle).delete();
      firebase.storage().ref(`gallery/${imageName}`).delete();
      console.log("deleted");
      document.getElementById(articleTitle).style.display = "none";

    },

    async deleteBlog(blogTitle){
      console.log(blogTitle)
      firebase.firestore().collection("blogs").doc(blogTitle).delete();
      document.getElementById(blogTitle).style.display = "none";

    },

    async login(){

      if(!document.getElementById('email').value || !document.getElementById('password').value){
        alert("fill out password and email fields")
      }
      else{
        await firebase.auth().signInWithEmailAndPassword(document.getElementById('email').value, document.getElementById('password').value)
        .then((userCredential) => {
          // Signed in 
          console.log("signed in")
          document.getElementById("loginForm").style.display = "none";
          document.getElementById("pageContent").style.display = "inline";
          const user = userCredential.user;

          this.getGalleryImages();
          this.getArticles();
          this.getBlogs();

          // ...
        })
        .catch((error) => {
          console.log(error)
          console.log("not signed in")
          alert("Email or password is wrong")

          const errorCode = error.code;
          const errorMessage = error.message;
        });
      }

    },

  uploadImage(){
    if (!document.getElementById('imageField').value) {
    console.log("no content")
    alert("Oops. It seems you didn't upload an image.")
    }
    else{
      console.log("clicked")
      this.img1=null;
      const imageUpload = document.getElementById('imageField').files[0];
      console.log(imageUpload);
      console.log("here");
      const storageRef=firebase.storage().ref(`gallery/${imageUpload.name}`).put(imageUpload);
      storageRef.on(`state_changed`,snapshot=>{
      this.uploadValue = (snapshot.bytesTransferred/snapshot.totalBytes)*100;
        }, error=>{console.log(error.message)},
      ()=>{this.uploadValue=100;
          storageRef.snapshot.ref.getDownloadURL().then((url)=>{
              this.img1 =url;
              console.log(this.img1);
              firebase.firestore().collection("gallery").doc(imageUpload.name).set({"url": this.img1});
            });
          }      
        );
      document.getElementById('imageField').value = ""
  }
 },
 uploadArticle(){
  if (!document.getElementById('articleImage').value || !document.getElementById('articleTitle').value || !document.getElementById('articleUrl').value || !document.getElementById('articleDesc').value) {
    console.log("no content")
    alert("Oops. It seems you didn't fill out all the fields for the article form.")
    }
  else{
    this.img1=null;
    const imageUpload = document.getElementById('articleImage').files[0];
    console.log(imageUpload);
    console.log("here");
    const storageRef= firebase.storage().ref(`news/${imageUpload.name}`).put(imageUpload);
    storageRef.on(`state_changed`,snapshot=>{
    this.uploadValue = (snapshot.bytesTransferred/snapshot.totalBytes)*100;
      }, error=>{console.log(error.message)},
    ()=>{this.uploadValue=100;
        storageRef.snapshot.ref.getDownloadURL().then((url)=>{
            this.img1 =url;
            console.log(this.img1);
            firebase.firestore().collection("news").doc(document.getElementById('articleTitle').value).set({"image": this.img1, title: document.getElementById('articleTitle').value, url: document.getElementById('articleUrl').value, desc: document.getElementById('articleDesc').value, imageName: imageUpload.name}).then(() =>{
              document.getElementById('articleImage').value = "";
              document.getElementById('articleTitle').value = "";
              document.getElementById('articleUrl').value = "";
              document.getElementById('articleDesc').value = "";
            });
          });
        }      
      );

  }
 },
 uploadBlog(){
  if (!document.getElementById('blogTitle').value || !document.getElementById('blogDate').value || !document.getElementById('blogText').value) {
    console.log("no content")
    alert("Oops. It seems you didn't fill out all the fields for the blog form.")
    }
  else{
    firebase.firestore().collection("blogs").doc(document.getElementById('blogTitle').value).set({title:document.getElementById('blogTitle').value, text: document.getElementById('blogText').value, date: document.getElementById('blogDate').value})
    document.getElementById('blogTitle').value = "";
    document.getElementById('blogDate').value = "";
    document.getElementById('blogText').value = "";

  }
}
  },
  head: {
    title: "Admin",
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
        content: "",
      },
      {
        hid: "og:title",
        name: "og:title",
        content: "Admin",
      },
      {
        property: "og:description",
        content: "",
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
#pageContent{
  display: none;
}
.accordion {
  background-color: #eee;
  color: #444;
  cursor: pointer;
  padding: 18px;
  width: 75%;
  text-align: center;
  border: none;
  outline: none;
  transition: 0.4s;
  display: flex;
  margin: 5px auto;
}
.deleteBtn {
  position: absolute;
  right: 18%;
	background: red;
}

.content{
  background-color: #eee;
  color: #444;
  cursor: pointer;
  padding: 18px;
  width: 75%;
  text-align: center;
  border: none;
  transition: 0.4s;
  display: flex;
  margin: 5px auto;

}
.contentBtn{
  background-color: #eee;
  color: #444;
  cursor: pointer;
  padding: 18px;
  width: 75%;
  text-align: center;
  border: none;
  transition: 0.4s;
  display: flex;
  margin: 5px auto;

}
.contentUpload{
  background-color: #8f00ff;
  cursor: pointer;
  transition: 0.4s;
  display: flex;
  margin: 5px auto;

}
</style>
