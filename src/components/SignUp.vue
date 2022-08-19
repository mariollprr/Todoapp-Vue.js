<template>
  <section class="vh-50 gradient-custom">
    <div class="container py-5 h-50">
      <div class="row d-flex justify-content-center align-items-center h-100">
        <div class="col-12 col-md-8 col-lg-6 col-xl-5">
          <div class="card bg-dark text-white" style="border-radius: 1rem">
            <div class="card-body p-5 text-center">
              <div class="mb-md-5 mt-md-4 pb-5">
                <h3>Welcome to</h3>
                <h1 class="mb-2">
                  OhMy<span class="fw-bold" id="texto"
                    ><strong><i>Tasks!</i></strong></span
                  >
                </h1>
                <h5 class="text-white-50 mb-5">
                  First task: Create your account
                  <img src="../assets/check.svg" alt="check" />
                </h5>
                <aside></aside>
                <div class="form-outline form-white mb-4">
                  <input
                    type="email"
                    id="typeEmailX"
                    class="form-control form-control-lg"
                    placeholder="Email"
                    :value="email"
                  />
                  <label class="form-label" for="typeEmailX">Email</label>
                </div>

                <div class="form-outline form-white mb-4">
                  <input
                    type="password"
                    id="typePasswordX"
                    class="form-control form-control-lg"
                    placeholder="********"
                    :value="password"
                  />
                  <label class="form-label" for="typePasswordX">Password</label>
                </div>

                <div class="form-outline form-white mb-4">
                  <input
                    type="password"
                    id="typeConfirmPasswordX"
                    class="form-control form-control-lg"
                    placeholder="********"
                    :value="password"
                  />
                  <label class="form-label" for="typeConfirmPasswordX"
                    >Confirm Password</label
                  >
                </div>

                <div>
                  <button
                    class="btn btn-outline-light btn-lg px-5"
                    type="submit"
                  >
                    Sign Up
                  </button>
                </div>

              </div>
              <PersonalRouter :route="route" :buttonText="buttonText"/>
            </div>
          </div>
        </div>
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
const buttonText = "Don’t have an account? Sing Up";

// Input Fields
const email = ref("");
const password = ref("");

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
const signIn = async () => {
  try {
    await useUserStore().signIn(email.value, password.value);
    redirect.push({ path: "/." });
  } catch (error) {
    errorMsg.value = `Error: ${error.message}`;
    setTimeout(() => {
      errorMsg.value = null;
    }, 5000);
  }
};
</script>

<style></style>
