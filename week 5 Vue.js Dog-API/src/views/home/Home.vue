<template>
  <div class="home">
    <h2 class="page-header">Home</h2>
    User : {{user}}
     <form @submit.prevent="update">
      <input type="text" placeholder="Name" v-model="name" />
      <br />
      <input type="text" placeholder="Last Name" v-model="lastname" />
      <br />
      <button type="submit">Guncelle</button>
    </form>
    
    
    form>
    <header class="home__header">
      <h3 class="home__title">
        Lorem ipsum dolor, sit amet consectetur adipisicing elit. Laudantium, dolor.
      </h3>
    </header>
  </div>
</template>

<script>
var firebaseConfig = {
    apiKey: "AIzaSyB2bAGSJ2HI-64FJ0kZJCPufSKh1hlnw1o",
    authDomain: "front-end-boot-camp.firebaseapp.com",
    projectId: "front-end-boot-camp",
    storageBucket: "front-end-boot-camp.appspot.com",
    messagingSenderId: "1009962707728",
    appId: "1:1009962707728:web:8c531b92fa7914fc609395",
    measurementId: "G-CEQS7QJD2Z"
  };
    firebase.initializeApp(firebaseConfig);

import { onMounted, onUnmounted, ref } from "vue";
export default {
  setup() {
    let user = ref({});
    let name = ref("");
    let lastname = ref("");
    const database = firebase.firestore();
    const test = database.collection("test");
    test.doc("1").onSnapshot(async function (data) {
      let result = data.data();
      user.value = result;
      console.log(result);
    });
    const update= ()=>{
      // test.doc("1").set({
      //   name = name.value,
      //   lastname = lastname.value,
      // });
    };
    onMounted(() => console.log("Mount: ⛰ Home Component"));
    onUnmounted(() => console.log("unMount: 👋🏻 Home Component "));

    return {
      user,
      name,
      lastname,
      update,
    };
  },
};
</script>

<style lang="scss">
.home {
  display: flex;
  flex-direction: column;
  align-items: stretch;
  justify-content: flex-start;

  &__header {
    flex-grow: 1;

    margin: 0;
    padding: 20px;

    min-height: 120px;

    display: flex;
    flex-direction: row;
    align-items: flex-start;
    justify-content: flex-start;

    background-color: $blue;
    color: $white;
  }
}
</style>
