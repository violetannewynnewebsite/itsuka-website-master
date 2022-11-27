<template>
  <div class="container animate__animated animate__fadeIn">
    <div class="row">
        <div class="priorities" style="font-size:22px;">
          <h1 class="line-after">Prioritising The Basics</h1>
          <h3>Housing</h3>
          <p>As somebody with first-hand experience of the rental market &amp; hidden homelessness, raising
a large family – I understand the housing crisis. I believe that the Right to Housing should be
a Human Right and that successive Governments and Action Plans have not adequately
delivered on this issue. I also believe that we need a clearer definition of homelessness, and
this is something I intend to legislate on. We also need to find meaningful alternatives to
emergency accommodation. Having people in hotels &amp; B&amp;Bs is not just unviable, it’s a waste
of your money -I will continue to challenge the Minister on this.</p>
          <p>We need the State to build houses. We need more social, affordable, cost-rental housing;
we need more transient housing; and we need for all of this housing to be accessible with
universal design We need for the vacant homes issue to be meaningfully tackled in County
Clare, and we need to increase the targets of the Repair &amp; Lease Scheme. These are my
priorities for Housing, and what I will advocate for on your behalf.</p>

          <h3>Healthcare For All</h3>
          <p>County Clare is incredibly underresourced when it comes to Healthcare. We have suffered
from a lack of funding and vision from the HSE, and a lack of interest from successive
Governments. We are below the national average in terms of GP and dental care availability,
and struggle to get an appointment if we have a medical card. We have suffered from over a
decade of no A&amp;E, reduced out-of-hours GP availability, and an ambulance service that
simply can’t keep up with demand.</p>
          <p>My priorities for healthcare are to extend the opening hours of the Ennis Injury Unit and
eventually build up to a full upgrade of Ennis to a Model 3 Hospital and reinstatement of our
A&amp;E Department, to support the Model 4 Teaching Hospital at UHL, as recommended by the
Health Information &amp; Quality Authority.</p>
          <p>On local and primary healthcare, I want to see the the Sláintecare plan fully funded and
service provision extended to stop people from having to take an unnecessary journey to the
A&amp;E in University Hospital Limerick, the most overcrowded in Ireland. I want to see
legislation changed to make it more attractive for GPs and dentists to set up in rural counties
like Clare, so that we can shrink the waitlists to be seen for basic medical queries. And most
importantly I want to give the people of Clare a fighting chance – and level the playing field
when it comes to equal access to healthcare.</p>
          <h3>Mental Health</h3>
          <p>It is crucial that we have access to supports and services for Mental Health in communities
throughout County Clare. These past few years of pandemic and lockdown have resulted in
feelings of mental and physical isolation for many in our society. Therefore is it vital that we
see a swift return and ramping up of in-person primary mental healthcare throughout County
Clare, this is a strong priority of mine in the Dáil.</p>
          <p>As a Parent of a child with special needs, I understand the pressures that many families of
children with additional needs face, and the fight they need to put up for basic services. I am
passionate about securing supports for our children’s development and for their families.  
I am a fighter, and every week in the Dáil, I fight to for adequate and consistent supoports in
our communities for our children and families. I use my time to advocate for the full
implementation of  both A Vision for Change (2006), and its successor; Sharing the Vision
(2020).</p>
          <p>In particular, we need additional funding for child &amp; young person mental health supports. My
record in supporting and demanding increased funding for CAMHS, the National Educational
Psychological Service and Early-Intervention Services will continously show that I am
committed to ensuring that Mental Health supports for our children and Youth are a priority.
Since my election, I have lobbied for enhanced funding for these essential services and will
continue to do so right throughout my term.</p>
          <h3>Disability</h3>
          <p>I am passionate about disability advocacy in all sectors of society. Since my election, I have
worked hand-in-hand with disability advocates and organisations in Clare and nationally to
push for the future proofing of access to disability services and universal design in house
building by the State. Previously I sat on the Joint Oireachtas Committee on Disability
Matters. The Comittee considers all disability issues including monitoring
the implementation by Ireland of the United Nations Convention on the Rights of People with
Disabilities, UNCRPD.</p>
          <p>I continue to advocate for and unequivocally support the ratification of the Optional Protocol
of the United Nations Convention on the Rights of People with Disabilities (UNCRPD), which
would enable people with disabilities to make complaints to the UN about potential violations
of their Human Rights and make their Human rights a reality. 
 The Optional Protocol must be ratified as a matter of urgency and should have been ratified
at the same time as the ratification of the UNCRPD. There must be no Further delays for
people with Disabilities, they have waited far too long for the basics.</p>

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
</style>
