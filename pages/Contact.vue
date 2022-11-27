<template>
  <b-container class="page animate__animated animate__fadeIn" style="font-size:22px;">
    <b-row class="justify-content-center">
      <b-col cols="md-6">
        <h2>Get in touch 💌</h2>

        <p class="text-left">
          If you have any question or just want to say hi, i'll try my best to
          get back to you.
        </p>
        <h3>Contact Details</h3>
        <p>Address 1: 64 Parnell street, Ennis, County Clare, V95 K33H, 065 6842251</p>
        <p>Address 2: Leinster House, Kildare street, Dublin 2, 01 6183088</p>
        <p>Email 📧: Violet-Anne.Wynne@oireachtas.ie</p>

      </b-col>
    </b-row>
  </b-container>
</template>
<script>
export default {
  data() {
    return {
      showAlert: false,
      formData: {
        name: "",
        email: "",
        message: "",
      },
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
    title: "Contact",
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
        content: "Do you have any enquires? Send a message now to my Developer",
      },
      {
        hid: "og:title",
        name: "og:title",
        content: "Contact - Itsuka",
      },
      {
        property: "og:description",
        content: "Do you have any enquires? Send a message now to my Developer",
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
