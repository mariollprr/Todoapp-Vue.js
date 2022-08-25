<template>
  <nav class="navbar navbar-expand-lg navbar">
    <!-- Container wrapper -->
    <div class="container">
      <!-- Navbar brand -->
      <router-link to="/">
        <img src="../assets/nav-logo.png" height="65" alt="OHMT logo" loading="lazy" style="margin-top: -1px;;" />
      </router-link>
      <!-- Collapsible wrapper -->
      <div class="collapse navbar-collapse" id="navbarButtonsExample">
        <!-- Left links -->
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <a class="nav-link" href="#"></a>
          </li>
        </ul>
        <div>
          <!-- Welcome message -->
          <p id="welcomemsg" class="me-auto"> <img
              src="../assets/kisspng-hand-waving-wave-emoji-clip-art-hand-wave-5b4ff8bd421f79.6030101615319676772709.png"
              width="22" height="22" alt="" /> Welcome back, <span>mario</span>!</p>
        </div>
        <!-- Sign out button -->
        <div class="d-flex align-items-right">
          <button @click="signOut" type="button" class="btn btn-primary me-3">
            Sign Out
          </button>
        </div>
      </div>
      <!-- Collapsible wrapper -->
    </div>
    <!-- Container wrapper -->
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
// const email = userStore.user.email;
// // constant that saves the user email and cleans out the @client from the user
// const name = email.split("@");
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