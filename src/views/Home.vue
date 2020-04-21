<template>
  <v-container>
<h1 class="text-center mb-8">GSAP ANIMATIONS</h1>
    <v-row>
      <h1>Simple bounce =></h1>
      <v-col>
        <transition
          appear
          @before-enter="beforeEnter"
          @enter="enter"
          :css="false"
        >
          <div class="card"></div>
        </transition>
      </v-col>
    </v-row>
    <v-row>
      <h1>Stagger =></h1>
      <v-col>
        <div id="container">
          <div v-for="card in cards" :key="card.id" class="card"></div>
        </div>
      </v-col>
    </v-row>

    <v-divider></v-divider>
    <v-divider></v-divider>
    <v-divider></v-divider>

    <v-row class="red mt-8">
      <v-col>
        <input v-model="newContact" placeholder="Name" type="text" />
        <button @click="addContact">Add Contact</button>

        <transition-group name="slide-up" tag="ul" appear>
          <li v-for="contact in contacts" :key="contact">
            {{ contact }}
          </li>
        </transition-group>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import gsap from "gsap";

export default {
  name: "Home",
  data() {
    return {
      newContact: "",
      contacts: ["Beau Thabeast", "Cindy Rella", "Alice Wunderlind"],
      cards: [
        { id: 1298 },
        { id: 8748 },
        { id: 4919 },
        { id: 5527 },
        { id: 9428 },
        { id: 7103 }
      ]
    };
  },
  mounted() {
    // stagger cards into position
    gsap.from('.card', {
    duration: 0.5,
    opacity: 0,
    scale: 0,
    y: 200,
    ease: 'power1',
    //stagger: 0.1
    stagger: {
        //from edges or center:
        from: 'edges',
        each: 0.1
      }
  })
  },
  methods: {
    beforeEnter(el) {
      // starting style
      el.style.opacity = 0;
      el.style.transform = "scale(0,0)";
    },
    enter(el, done) {
      // style to transition to once entered
      gsap.to(el, {
        duration: 1,
        opacity: 1,
        scale: 1,
        onComplete: done,
        ease: "bounce.out"
      });
    },
    addContact() {
      this.contacts.push(this.newContact);
      this.newContact = "";
    },
    sortContacts() {
      this.contacts = this.contacts.sort();
    }
  }
};
</script>
<style lang="scss" scoped>
#container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-evenly;
}
.card {
  display: block;
  margin: 0 auto 0 auto;
  height: 6.5em;
  width: 6.5em;
  border-radius: 1%;
  background-color: #16c0b0;
  box-shadow: 0.08em 0.03em 0.4em #ababab;
}
</style>