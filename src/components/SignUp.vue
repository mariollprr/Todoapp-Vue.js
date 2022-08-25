<template>
  <section>
    <div class="row g-0 align-items-center">
      <div class="col-lg-6 mb-5 mb-lg-0">
        <div class="card cascading-right" style="
            background: hsla(0, 0%, 100%, 0.55);
            backdrop-filter: blur(30px);
            ">
          <div class="card-body p-5 shadow-5 text-center">
            <div class="logo text-center">
              <img src="../assets/sign-logo.png" alt="logo ohmytasks!" class="logoimg" width="200" height="200" />
              <h5 class=" mb-5">SIGN UP FOR YOUR ACCOUNT</h5>
            </div>
            <form @submit.prevent="signUp">
              <label class="form-label" for="form3Example3">Email</label>
              <div class="form-outline mb-4">
                <input type="email" id="form3Example3" class="form-control" placeholder="example@email.com"
                  v-model="email" required />
              </div>
              <label class="form-label" for="form3Example4">Password</label>
              <div class="input-group mb-3">
                <input required v-model="password" class="form-control" :type="passwordFieldType"
                  placeholder="**********" id="exampleInputPassword1" />
                <div class="btn btn-light">
                  <i v-if="!hidePassword" @click="hidePassword = !hidePassword" class="fa-solid fa-eye"></i>
                  <i v-else @click="hidePassword = !hidePassword" class="fa-solid fa-eye-slash"></i>
                </div>
                <div>
                </div>
              </div>
              <label class="form-label" for="exampleInputPassword1">Confirm password</label>
              <div class="input-group mb-3">
                <input required v-model="confirmPassword" class="form-control" :type="passwordFieldType"
                  placeholder="**********" id="exampleInputPassword1" />
                <div class="btn btn-light">
                  <i v-if="!hidePassword" @click="hidePassword = !hidePassword" class="fa-solid fa-eye"></i>
                  <i v-else @click="hidePassword = !hidePassword" class="fa-solid fa-eye-slash"></i>
                </div>
                <div>
                </div>
              </div>
              <p v-if="errorMsg" class="alert alert-danger" role="alert">{{ errorMsg }}</p>
              <button type="submit" class="btn btn-primary btn-block mb-4">
                Sign Up
              </button>
              <div class="text-center">
                <div>
                  <p>Have an account?
                    <PersonalRouter :route="route" :buttonText="buttonText" />
                  </p>
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>
      <div class="col-lg-6 mb-5 mb-lg-0">
        <img src="../assets/undraw_trip.svg" class="w-100 rounded-4 shadow-4" alt="Welcome image" height="746" />
      </div>
    </div>
  </section>
</template>

<script setup>
import PersonalRouter from "./PersonalRouter.vue";
import { ref, computed } from "vue";
import { supabase } from "../supabase";
import { useRouter } from "vue-router";
import { useUserStore } from "../stores/user";
import { storeToRefs } from "pinia";

// Route Variables
const route = "/auth/login";
const buttonText = "Sign In";
// Input Fields
const email = ref("");
const password = ref("");
const confirmPassword = ref("");
// Error Message
const errorMsg = ref("");
// Show hide password variable
const passwordFieldType = computed(() =>
  hidePassword.value ? "password" : "text"
);
const hidePassword = ref(true);
// Show hide confrimPassword variable
const hideconfirmPassword = ref(true);
// Router to push user once SignedUp to Log In
const redirect = useRouter();
// Arrow function to SignUp user to supaBase with a timeOut() method for showing the error
const signUp = async () => {
  if (password.value === confirmPassword.value) {
    try {
      // calls the user store and send the users info to backend to logIn
      await useUserStore().signUp(email.value, password.value);
      // redirects user to the homeView
      redirect.push({ path: "/auth/login" });
    }
    catch (error) {
      // displays error message
      errorMsg.value = "The email or password you entered is incorrect, please try again.";
      // hides error message
      setTimeout(() => {
        errorMsg.value = null;
      }, 5000);
    }
    return;
  }
  errorMsg.value = "Invalid token";
};
</script>

<style>
</style>
