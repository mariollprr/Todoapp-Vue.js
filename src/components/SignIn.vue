<template>
  <section class="min-height">
    <div class="row g-0 align-items-center">
      <div class="col-lg-6 mb-5 mb-lg-0">
        <div class="card cascading-right" style="
            background: hsla(0, 0%, 100%, 0.55);
            backdrop-filter: blur(30px);
            ">
          <div class="card-body p-5 shadow-5 text-center">
            <div class="text-center">
              <img src="../assets/sign-logo.png" alt="Logo OhMyTasks!" width="200" height="200" />
              <h5 class=" mb-5"><i>For people who forget to use to-do apps</i></h5>
            </div>
            <form @submit.prevent="signIn">
            <label class="form-label" for="form3Example3">Email</label>
              <div class="form-outline mb-4">
                <input type="email" id="form3Example3" class="form-control shadow-5" placeholder="example@email.com"
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
              <div class="sign-in-button">
                <p v-if="errorMsg" class="alert alert-danger" role="alert">{{ errorMsg }}</p>
                <button type="submit" class="btn btn-primary btn-block mb-4">Sign In</button>
              </div>
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
        <img src="../assets/work_from_anywhere.svg" class="w-100 rounded-4 shadow-4" alt="Welcome image" height="746" />
      </div>
    </div>
  </section>
  <Footer />
</template>

<script setup>
import Footer from "./Footer.vue";
import { ref, computed } from "vue";
import PersonalRouter from "./PersonalRouter.vue";
import { supabase } from "../supabase";
import { useRouter } from "vue-router";
import { useUserStore } from "../stores/user";
import { storeToRefs } from "pinia";

// Route Variables
const routeup = "/auth/sign-up";
const buttonTextup = "Sign Up";

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
    errorMsg.value = "The email or password you entered is incorrect, please try again.";
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

h5 {
  color: #2f2e41;
  margin-top: -20PX;
}

.btn-light {
  box-shadow: 6px 6px 5px 0px rgba(212, 212, 212, 1);
  width: 37px;
  height: 37px;
}

.form-control {
  box-shadow: 6px 6px 5px 0px rgba(212, 212, 212, 1);
  margin-bottom: 20px;;
}

.form-label {
  margin-bottom: 0;;
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
