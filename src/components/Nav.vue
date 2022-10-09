<template>
    <div>
      <router-link to="/">
        <img src="../assets/logo-horizontal.svg" alt="Logo OMTK!" />
      </router-link>
      <nav id="main-menu" class="main-menu">
        <ul>
          <li>
            <p id="welcomemsg" class="">
              Welcome back, <span>{{ name[0] }}</span>!
            </p>
          </li>
          <li><button @click="signOut" type="button">
              Sign Out
            </button>
          </li>
        </ul>
      </nav>
    </div>
</template>

<script setup>
import { useRouter } from "vue-router";
import { useUserStore } from "../stores/user";

const route = "/";
const redirect = useRouter();
const userStore = useUserStore();

const email = userStore.user.email;
// constant that saves the user email and cleans out the @client from the user
const name = email.split("@");

// Function to Sign Out
const signOut = async () => {
  try {
    // calls the user store and signs out
    await useUserStore().signOut();
    redirect.push({ path: "/auth/login" });
  } catch (error) {
    errorMsg.value = error.message;
    setTimeout(() => {
      errorMsg.value = null;
    }, 5000);
  };
};
</script>

<style>

</style>