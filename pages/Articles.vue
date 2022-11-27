<template>
  <b-container class="page  animate__animated animate__fadeIn">
    <h2 align="left" class="line-after">Recent Articles</h2>

    <b-row class="articles" v-if="blogs.length > 0" style="font-size:20px;">
      <div class="col-md-6" v-for="blog in blogs" :key="blog.id">
        <div>
          <b-card-group deck>
            <b-card
              :img-src="blog.image"
              :img-alt="blog.imgAlt"
              img-top
              tag="article"
              class="mb-2"
            >
              <h4>{{ blog.title }}</h4>
              <b-badge
                class="animate__animated animate__fadeInUp"
                style="margin: 2px;"
                v-for="tag in blog.tags"
                :key="tag"
                pill
                :variant="
                  tagVariants[Math.floor(Math.random() * tagVariants.length)]
                "
                >#{{ tag }}</b-badge
              >
              <hr />
              <b-card-text>{{ blog.desc }}</b-card-text>

              <b-button
                :href="blog.url"
                target="_blank"
                rel="noopener"
                variant="default"
                >Read More..</b-button
              >
            </b-card>
          </b-card-group>
        </div>
      </div>
    </b-row>
  </b-container>
</template>
<script>
import HeartIcon from "vue-ionicons/dist/md-heart.vue";
import firebase from "firebase";

export default {
  components: { HeartIcon },
  data() {
    return {
      showLoader: true,
      showErrALert: false,
      tagVariants: ["primary", "success", "warning", "info", "dark", "danger"],
      blogs: []
    };
  },
  head: {
    title: "Latest News",
    meta: [
      {
        hid: "description",
        name: "description",
        content:
          "Read articles written about Violet-Anne Wynne."
      },
      {
        hid: "og:title",
        name: "og:title",
        content: "Recent Articles"
      },
      {
        property: "og:description",
        content: "Read articles written about Violet-Anne Wynne."
      },
    ]
  },
  methods: {
    // get articles hosted on dev.to
    getArticles() {
      firebase.firestore().collection("news").get().then((querySnapshot) => {
      querySnapshot.forEach((doc) =>{
        this.blogs.push({
          title: doc.data().title,
          desc: doc.data().desc,
          image: doc.data().image,
          url: doc.data().url
        }
        );
      });
    })

      
      // fetch("https://dev.to/api/articles?username=" + username)
      //   .then(res => res.json())
      //   .then(data => {
      //     data.forEach(article => {
      //       if (/(hcti.io)/.test(article.image) == true) {
      //         // use random image from lorem picsum
      //         articleImage = "https://picsum.photos/600/400";
      //       } else {
      //         articleImage = article.social_image;
      //       }
      //       this.blogs.push({
      //         id: article.id,
      //         title: article.title,
      //         desc: article.description,
      //         image: articleImage,
      //         url: article.url,
      //         date: article.readable_publish_date,
      //         tags: article.tag_list,
      //         imgAlt: article.title + " - Asaolu Elijah"
      //       });
      //     });
      //     success();
      //   })
      //   .catch(err => {
      //     error();
      //     console.log("Error fetching articles " + err);
      //   });
    }
  },
  mounted() {
    this.getArticles(
      "asaoluelijah",
      () => {
        this.showLoader = false;
      },
      () => {
        this.showErrALert = true;
        this.showLoader = false;
      }
    );
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

    // firebase.firestore().collection("gallery").doc(imageUpload.name).set({"url": this.img1});

    
  }
};
</script>
<style scoped>
.container {
  margin-top: 120px;
}
.row {
  margin-top: 40px;
}
.spinner-border {
  margin-top: 40px;
}
.card {
  text-align: left;
  color: #000;
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
