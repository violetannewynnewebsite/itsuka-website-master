<template>
  <div class="container animate__animated animate__fadeIn">
    <div class="row">
        <div class="about textBackground" style="font-size:22px;">
          <h1 class="line-after">About Me</h1>
          <h4 class="mt-4">Hey 👋</h4>
          <p class="textBackground">
            My name is Violet-Anne Wynee, I am a <b>TD </b> from Clare.
          </p>
          <p>I am 35 and a mother of six Children. My third born Travis was diagnosed with Autism in January
2017. Before getting Elected in 2020, I was a carer for my son Travis and receiving the carers
allowance from the Dept. Of Social Protection.</p>
          <img src="../assets/about1.webp" style="width:60%; height:auto;   display: block; margin-left: auto; margin-right: auto;"/>
          <p style="margin-top: 30px;">I completed my BA in Single Honours Psychology from Trinity College Dubln in 2009, receiving a 2:1
          Honours degree. I completed the Trinity Access Programme in 2008. I volunteered for the
          CrimeVictims Helpline and worked for a Home Help service for children and adolecents with
          disabilities.</p>
          <img src="../assets/about2.png" style="width:60%; height:auto;  display: block; margin-left: auto; margin-right: auto;"/>
          <p>In raising my children and moving to Rural Clare I experienced the difficulties that so many do with
Public Transport and the difficulties that causes in accessing services such as Maternity Care and
support services for my son, just as examples as there are many more.</p>
          <img src="../assets/about3.png" style="width:60%; height:auto;  display: block; margin-left: auto; margin-right: auto;"/>  
            <p>I went into Politics <b> to make changes </b> from lived experience and with the intention of speaking for the
people of Clare, especially those who are marganlised the most. I also wanted to crush societal
norms by speaking about my past experiences without shame and with full transparency. Nothing is
as it seems and I would love to live in a society that is free from judgement, that is open and able to
progress for needs of the individual.</p>
        </div>
      </div>
    </div>
</template>
<script>
export default {
  data() {
    return {
      startYear: 2022,
      currYear: new Date().getFullYear(),
      stacks: [
        {
          language: "HTML",
          experience: "3+ Years",
          variant: "secondary",
          breif: "lorem...",
        },
        {
          language: "CSS",
          experience: "3+ Years",
          variant: "primary",
          breif: "lorem...",
        },
        {
          language: "Javascript",
          experience: "2+ Years",
          variant: "warning",
          breif: "lorem...",
        },
        {
          language: "VUE.JS",
          experience: "2+ Years",
          variant: "success",
          breif: "lorem...",
        },
        {
          language: "Node.js",
          experience: "2+ Years",
          variant: "dark",
          breif: "lorem...",
        },
      ],
    };
  },
  head: {
    title: "About",
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
        // currYear - startYear
        content: `A Lightweight and Stable Discord Music Bot For Your Daily Production.`,
      },
    ],
  },
};
</script>
<style scoped>
.container {
  margin-top: 140px;
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
.abt-img {
  width: inherit;
  height: inherit;
  border-radius: 5px;
}
/* .abt-img:hover {
  animation: swing;
  animation-duration: 2s;
} */
textBackground{
  background-color: #000;
}
</style>
