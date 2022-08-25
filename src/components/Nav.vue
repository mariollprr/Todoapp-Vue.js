<template>
  <!-- <nav class="navbar navbar-expand-lg navbar">
    <div class="container">
      <router-link to="/">
        <img src="../assets/nav-logo.png" height="65" alt="OHMT logo" loading="lazy" style="margin-top: -1px;;" />
      </router-link>
      <div class="collapse navbar-collapse" id="navbarButtonsExample">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <a class="nav-link" href="#"></a>
          </li>
        </ul>
        <div>
          <p id="welcomemsg" class="me-auto"> <img
              src="../assets/kisspng-hand-waving-wave-emoji-clip-art-hand-wave-5b4ff8bd421f79.6030101615319676772709.png"
              width="22" height="22" alt="" /> Welcome back, <span>{{ name[0] }}</span>!</p>
        </div>
        
      </div>
    </div>
  </nav> -->
  <nav class="navbar navbar-expand-lg ">
    <div class="container-fluid">
      <router-link to="/">
        <img src="../assets/nav-logo.png" height="65" alt="OHMT logo" loading="lazy" style="margin-top: -1px;;" />
      </router-link>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarText"
        aria-controls="navbarText" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarText"> <p id="welcomemsg" class="me-auto"> <img
            src="../assets/kisspng-hand-waving-wave-emoji-clip-art-hand-wave-5b4ff8bd421f79.6030101615319676772709.png"
            width="22" height="22" alt="" /> Welcome back, <span>{{ name[0] }}</span>!</p>
            <div class="d-flex align-items-right">
          <button @click="signOut" type="button" class="btn btn-primary me-3">
            Sign Out
          </button>
        </div>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { useRouter } from "vue-router";
import { supabase } from "../supabase";
import { useUserStore } from "../stores/user";
//constant to save a variable that will hold the use router method
const route = "/";
// constant to save a variable that will get the user from store with a computed function imported from vue
const userStore = useUserStore();
// constant that calls user email from the useUSerStore
const email = userStore.user.email;
// constant that saves the user email and cleans out the @client from the user
const name = email.split("@");
// async function that calls the signOut method from the useUserStore and pushes the user back to the Auth view.
const redirect = useRouter();
const signOut = async () => {
  try {
    // calls the user store and signs out
    await useUserStore().signOut();
    // redirects user to the auth login
    redirect.push({ path: "/auth/login" });
  } catch (error) {
    // displays error message
    errorMsg.value = error.message;
    // hides error message
    setTimeout(() => {
      errorMsg.value = null;
    }, 5000);
  };
};
</script>

<style>
#welcomemsg {
  margin-top: 20px;
  color: white;
  padding-right: 30px
}

img {
  margin-top: -1px;
}

span {
  font-weight: bold;
}

.navbar-expand-lg {
  background-color: #2f2e41;
}
</style>