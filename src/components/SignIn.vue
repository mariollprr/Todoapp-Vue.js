<template>
  <section class="min-height">
    <div class="row g-0 align-items-center">
      <div class="col-lg-6 mb-5 mb-lg-0">
        <div class="card cascading-right" style="
            background: hsla(0, 0%, 100%, 0.55);
            backdrop-filter: blur(30px);
            ">
          <!-- Logo -->
          <div class="card-body p-5 shadow-5 text-center">
            <div class="text-center">
              <img src="../assets/1.png" alt="logo ohmytasks!" width="200" height="150" />
              <h6 class=" mb-5"><i>For people who forget to use to-do apps</i></h6>
            </div>
            <!-- Fornm -->
            <form @submit.prevent="signIn">
              <!-- Email input -->
              <div class="form-outline mb-4">
                <input type="email" id="form3Example3" class="form-control shadow-5" placeholder="example@email.com"
                  v-model="this.email" required />
                <label class="form-label" for="form3Example3">Email address</label>
              </div>
              <!-- Password input -->
              <div class="form-outline mb-4">
                <input type="password" id="form3Example4" class="form-control shadow-5" placeholder="*********"
                  v-model="this.password" />
                <label class="form-label" for="form3Example4">Password</label>
              </div>
              <!-- Submit button -->
              <button type="submit" class="btn btn-primary btn-block mb-4">
                Sign In
              </button>
              <!-- Register buttons -->
              <div class="text-center">
                <div>
                  <p>Don't have an account?
                    <PersonalRouter :route="routeup" :buttonText="buttonTextup" />
                  </p>
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>
      <div class="col-lg-6 mb-5 mb-lg-0">
        <img src="../assets/work_from_anywhere.svg" class="w-100 rounded-4 shadow-4"
          alt="Welcome image" height="746" />
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from "vue";
import PersonalRouter from "./PersonalRouter.vue";
import { supabase } from "../supabase";
import { useRouter } from "vue-router";
import { useUserStore } from "../stores/user";
import { storeToRefs } from "pinia";

// Route Variables
const routeup = "/auth/sign-up";
const buttonTextup = "Sign up";

// Input Fields
const email = ref("");
const password = ref("");

// Error Message
const errorMsg = ref("");

//Show hide password variables
const passwordFieldType = computed(() =>
  hidePassword.value ? "password" : "text"
);
const hidePassword = ref(true);
// Router to push user once SignedIn to the HomeView
const redirect = useRouter();

// Arrow function to Signin user to supaBase
const signIn = async () => {
  try {
    // calls the user store and send the users info to backend to logIn
    await useUserStore().signIn(email.value, password.value);
    // redirects user to the homeView
    redirect.push({ path: "/" });
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
a {
  text-decoration: none;
  font-weight: 600;
}

.cascading-right {
  margin-right: -50px;
}

@media (max-width: 991.98px) {
  .cascading-right {
    margin-right: 0;
  }
}
</style>
