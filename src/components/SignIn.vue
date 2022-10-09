<template>
  <section class="">
    <div class="">
      <div class="">
        <img src="../assets/logo-vertical.svg" alt="Logo OhMyTasks!" width="200" height="200" />
        <h5 class="">For people who forget to use to-do apps</h5>
      </div>
      <form @submit.prevent="signIn">
        <label class="" for="form3Example3">Email</label>
        <div class="">
          <input type="email" id="form3Example3" class="" v-model="email" required />
        </div>
        <label class="" for="form3Example4">Password</label>
        <div class="">
          <input v-model="password" class="" :type="passwordFieldType" id="exampleInputPassword4" required />
          <div class="">
            <i v-if="!hidePassword" @click="hidePassword = !hidePassword" class="fa-solid fa-eye"></i>
            <i v-else @click="hidePassword = !hidePassword" class="fa-solid fa-eye-slash"></i>
          </div>
          <div>
          </div>
        </div>
        <div class="">
          <p v-if="errorMsg" class="" role="alert">{{ errorMsg }}</p>
          <button type="submit" class="">Sign In</button>
        </div>
        <div class="">
          <div>
            <p>Don't have an account?
              <PersonalRouter :route="routeUp" :buttonText="buttonTextUp" />
            </p>
          </div>
        </div>
      </form>
    </div>
    <div class="">
      <img src="" class="" alt="" />
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from "vue";
import PersonalRouter from "./PersonalRouter.vue";
import { useRouter } from "vue-router";
import { useUserStore } from "../stores/user";

// Route Variables
const routeUp = "/auth/sign-up";
const buttonTextUp = "Sign Up";
const redirect = useRouter();

// Input Fields
const email = ref("");
const password = ref("");

// Error message
const errorMsg = ref("");

// Show hide password 
const passwordFieldType = computed(() =>
  hidePassword.value ? "password" : "text"
);
const hidePassword = ref(true);

// Function to Sing In
const signIn = async () => {
  try {
    await useUserStore().signIn(email.value, password.value);
    redirect.push({ path: "/" });
  } catch (error) {
    errorMsg.value = "The email or password you entered is incorrect, please try again.";
    setTimeout(() => {
      errorMsg.value = null;
    }, 5000);
  };
};
</script>

<style></style>