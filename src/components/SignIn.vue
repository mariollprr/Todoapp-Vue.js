<template>
  <section class="vh-50 gradient-custom">
    <div class="container py-5 h-50">
      <div class="row d-flex justify-content-center align-items-center h-100">
        <div class="col-12 col-md-8 col-lg-6 col-xl-5">
          <div class="card bg-dark text-white" style="border-radius: 1rem">
            <div class="card-body p-5 text-center">
              <div class="mb-md-5 mt-md-4 pb-5">
                <h1 class="mb-2">
                  <i>OhMy</i
                  ><span class="fw-bold" id="texto"
                    ><strong><i>Tasks!</i></strong></span
                  >
                </h1>
                <h4 class="text-white-50 mb-5">
                  <quote>For people who forget to use to-do apps</quote>
                  <img src="../assets/check.svg" alt="check" />
                </h4>
                <aside></aside>
                <div class="form-outline form-white mb-4">
                  <input
                    type="email"
                    id="typeEmailX"
                    class="form-control form-control-lg"
                    placeholder="Email"
                  />
                  <label class="form-label" for="typeEmailX">Email</label>
                </div>

                <div class="form-outline form-white mb-4">
                  <input
                    type="password"
                    id="typePasswordX"
                    class="form-control form-control-lg"
                    placeholder="********"
                  />
                  <!-- <button onclick="switchVisibility()">show / hide</button> -->

                  <label class="form-label" for="typePasswordX">Password</label>
                </div>

                <div>
                  <button
                    class="btn btn-outline-light btn-lg px-5"
                    type="submit"
                  >
                    Sign In
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
import { ref, computed } from "vue";
import PersonalRouter from "./PersonalRouter.vue";
import { supabase } from "../supabase";
import { useRouter } from "vue-router";
import { useUserStore } from "../stores/user";
import { storeToRefs } from "pinia";

// Route Variables
const route = "/auth/sign-up";
const buttonText = "Don't have an account? Sing up";

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
    redirect.push({ path: "/." });
  } catch (error) {
    // displays error message
    errorMsg.value = `Error: ${error.message}`;
    // hides error message
    setTimeout(() => {
      errorMsg.value = null;
    }, 5000);
  }
};
</script>

<style>
p {
  padding-top: 70px;
  padding-bottom: 0;
}
#texto {
  background: linear-gradient(#1f8867, rgb(10, 255, 198));
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}
h1 {
  padding-bottom: 30px;
}

.gradient-custom {
  /* fallback for old browsers */
  background: #13ac7e;

  /* Chrome 10-25, Safari 5.1-6 */
  background: -webkit-linear-gradient(to right, #1f8867, rgb(10, 255, 198));

  /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  background: linear-gradient(to right, #0a7052, rgb(82, 236, 200));
}
span {
  font-size: 1.5em;
}
.form {
  display: flex;
  flex-direction: column;
  margin: 1rem 0;
}
input {
  color: white;
  text-decoration: none;
  margin-bottom: 1rem;
}
.button {
  border: none;
  color: white;
  padding: 10px 10px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
}
</style>
