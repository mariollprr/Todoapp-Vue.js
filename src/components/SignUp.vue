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
              <!-- Email input -->
              <div class="form-outline mb-4">
                <input type="email" id="form3Example3" class="form-control" placeholder="example@email.com"
                  v-model="email" required/>
                <label class="form-label" for="form3Example3">Email</label>
              </div>
              <!-- Password input -->
              <div class="form-outline mb-4">
                <input type="password" id="form3Example4" class="form-control" placeholder="*********"
                  v-model="password" required/>
                <label class="form-label" for="form3Example4">Password</label>
              </div>
              <!-- Confirm password input -->
              <div class="form-outline mb-4">
                <input type="password" id="form3Example5" class="form-control" placeholder="*********"
                  v-model="confirmPassword" required />
                <label class="form-label" for="form3Example4">Confirm password</label>
              </div>
              <!-- Submit button -->
              <button type="submit" class="btn btn-primary btn-block mb-4">
                Sign Up
              </button>
              <!-- Register buttons -->
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
        <img src="../assets/undraw_trip.svg" class="w-100 rounded-4 shadow-4"
          alt="Welcome image" height="746" />
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
      errorMsg.value = error.message;
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
